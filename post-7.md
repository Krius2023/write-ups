*   Syntax
    

```javascript
----
TYPE
----

type TUser = {
    userId: string,
    name: string,
    phoneNumber: string,
    userType: string
}

---------
INTERFACE
---------

interface IUser {
    userId: string,
    name: string,
    phoneNumber: string,
    userType: string
}
```

*   Declaration
    

```javascript
----
TYPE
----

// primitive types (number, string, boolean), tuples
type Tnum = number
type TPoint = [number, number]
type TObject = {
    name: string,
    id: string
}

---------
INTERFACE
---------

// only objects
interface IObject {
    name: string,
    id: string
}
```

*   Union / Intersection --- Extending
    

```javascript
----
TYPE
----

type TAdmin = TUser & {
    permissions: Array<string>
}
type TCustomer = TUser & {
    orders: Array<string>,
    cart: Array<string>
}
type TLoginUser = TAdmin | TCustomer

---------
INTERFACE
---------

interface IAdmin extends IUser {
    permissions: Array<string>
}
interface ICustomer extends IUser {
    orders: Array<string>,
    cart: Array<string>
}
type LoginUser = IAdmin | ICustomer
// using type in union/intersection cases
```

*   Utility Types - Ref: [https://www.typescriptlang.org/docs/handbook/utility-types.html](https://www.typescriptlang.org/docs/handbook/utility-types.html), Here it has given about `Omit` for example
    

```javascript
----
TYPE
----

type TTestUser = Omit<TUser, 'address' | 'phoneNumber'>;

---------
INTERFACE
---------

type OmittedProperties = 'address' | 'phoneNumber';
interface ITestUser extends Omit<IUser, OmittedProperties> { }
```

*   Tuple declaration
    

```javascript
----
TYPE
----

type TTuple = [number, string, boolean]

---------
INTERFACE
---------

interface ITuple {
    0: number,
    1: string,
    2: boolean
}
```
