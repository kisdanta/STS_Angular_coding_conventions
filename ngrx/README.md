# STS_Angular_coding_conventions-

1. Structure

```
- state (contains the type definition of the store and initialState)

- reducers (contains the reducers)

- actions (contains the actions)

- selectors (contains named selectors)

- effects (contains the effects class)

- adapters - optional (contains the adapters)
```

2. File naming

>It is better to prefix these filenames with the name of the feature they belong to

Bad
```
state.ts / selectors.ts / effects.ts ...
```

Good
```
person.selectors.ts
person.effects.ts
```

3. Keep a string enum of your feature names

Bad
```ts
@NgModule({
    StoreModule.forFeature({'user': userReducer}),
})
export class UserModule {}

const bookmarks = createFeatureSelector('user');
```

Good
```ts
export enum Features {
    User = 'user',
    Article = 'article',
    Bookmark = 'bookmark'
}

@NgModule({
    StoreModule.forFeature({[Features.User]: userReducer}),
})
export class UserModule {}

const bookmarks = createFeatureSelector(Features.User);
```

4. (Almost) never subscribe to Store

Bad
```ts
@Component({
    template: `
    <span>{{ name }}</span>
  `
})
export class ComponentWithStore implements OnInit, OnDestroy {
    name = '';

    $destroy = new Subject<void>();

    constructor(store: Store<AppState>) {}

    ngOnInit() {
        this.store
            .pipe(takeUtil($destroy))
            .subscribe(state => this.name = state.name);
    }
    
    ngOnDestroy() {
        this.$destroy.next();
        this.$destroy.complete();
    }
}
```

Good
```ts
@Component({
    template: `
    <span>{{ name$ | async }}</span>
  `
})
export class ComponentWithStore {
    name$ = this.store.select(state => state.name);

    constructor(store: Store<AppState>) {}
}
```

5. Handle logic code inside effect if you can

Bad
```ts
@Component({
    template: `
    <span>{{name}}</span>
  `
})
export class ComponentWithStore implements OnInit {
    name = '';

    constructor(store: Store<AppState>) {}

    ngOnInit() {
        this.store.subscribe(state => {
            if (state.name === 'ReservedName') {
                this.store.dispatch(reservedNameEncountered());
            }
        });
    }
}
```

Good
```ts
export class Effects {
    reservedName$ = createEffect(() => this.actions$.pipe(
        ofType(actions.setName),
        filter(({payload}) => payload === 'ReservedName'),
        map(() => reservedNameEncountered())
    ));

    constructor(actions$: Actions) {}
}
```

6. Don't pipe the Observable selected from the store

Bad
```ts
export class ComponentWithStore {
    activeUsers$ = this.store.select(state => state.users).pipe(
        map(users => users.filter(user => user.isActive)),
    );

    constructor(store: Store<AppState>) {}
}
```

Good
```ts
// selectors.ts
const activeUsers = (state: AppState) => state.users.filter(user => user.isActive)
```

7. Don't use combineLatest. Use named selectors instead

Bad
```ts
export class ClothingItemListComponent {
    clothingItems$ = combineLatest([
        this.store.select(state => state.clothingItems),
        this.store.select(state => state.cart),
    ]).pipe(
        map(([items, cart]) => items.map(item => ({
            ...item,
            isInShoppingCart: cart.map(cartItem => cartItem.id).includes(item.id),
        })))
    );

    constructor(store: Store<AppState>) {}
}
```

Good
```ts
const allItems = (state: AppState) => state.clothingItems;

const shoppingCart = (state: AppState) => state.shoppingCart;

const cartIds = createSelector(shoppingCart, cart => cart.map(item => item.id));

const clothingItems = createSelector(
    allItems,
    cartIds,
    (items, cart) => items.map(item => ({
            ...item,
            isInShoppingCart: cart.includes(item.id),
        }),
    );
```

8. Use selectors for the derived state

Bad
```ts
export const musiciansReducer = createReducer(
    on(musiciansPageActions.search, (state, { query }) => {
        // `filteredMusicians` is derived from `musicians` and `query`
        const filteredMusicians = state.musicians.filter(({ name }) =>
            name.includes(query)
        );

        return {
            ...state,
            query,
            filteredMusicians,
        };
    }))
);
```

Good
```ts
export const musiciansReducer = createReducer(
    on(musiciansPageActions.search, (state, { query }) => ({
        ...state,
        query,
    }))
);

export const selectFilteredMusicians = createSelector(
    selectAllMusicians,
    selectMusicianQuery,
    (musicians, query) =>
        musicians.filter(({ name }) => name.includes(query))
);
```

9. Don't dispatch actions conditionally

Bad

```ts
ngOnInit(): void {
    this.store.select(selectSongs).pipe(
        tap((songs) => {
            // if the songs are not loaded
            if (!songs) {
                // then dispatch the `loadSongs` action
                this.store.dispatch(songsActions.loadSongs());
            }
        }),
        take(1)
    ).subscribe();
}
```

Good

```ts
ngOnInit(): void {
    this.store.dispatch(songsPageActions.opened());
}

readonly loadSongsIfNotLoaded$ = createEffect(() => {
  return this.actions$.pipe(
    // when the songs page is opened
    ofType(songsPageActions.opened),
    // then select songs from the store
    concatLatestFrom(() => this.store.select(selectSongs)),
    // and check if the songs are loaded
    filter(([, songs]) => !songs),
    // if not, load songs from the API
    exhaustMap(() => {
      return this.songsService.getSongs().pipe(
        map((songs) => songsApiActions.songsLoadedSuccess({ songs })),
        catchError((error: { message: string }) =>
          of(songsApiActions.songsLoadedFailure({ error }))
        )
      );
    })
  );
});
```

10. Should put State on each action of reducer

Bad
```ts
interface State {
    users: User[];
    books: Book[];
    total: number;
}

export const reducer = createReducer(
    on(addUser, (state, user)) => ({
     ...state,
     users: [...state.users, user]
    })
);
```

Good
```ts
interface State {
    users: User[];
    books: Book[];
    total: number;
}

export const reducer = createReducer(
    on(addUser, (state, user)): State => ({
     ...state,
     users: [...state.users, user]
    })
);
```

