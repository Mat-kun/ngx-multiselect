# NgxMultiselect

Angular recursive select tree

-   [What is It ?](#what-is-it-?)
-   [Installation](#installation)
-   [Usage](#usage)
-   [Basic](#basic)
-   [Configuration](#configuration)

## What is it ?

NgxMultiSelect is a recursive select tree.
You can select one or multiple item in tree and they're returned in an array of items.
NgxMultiSelect can be configured for changing button's label.

## Installation

```shell
npm install @zokelion/ngx-multiselect --save

```

## Usage

### Basic

NgxMultiselect generate a tree based on an list of items.
the component should be declared in your html code like this :

```html
<ngx-multiselect
    (itemSelected)="getSelectedItem($event)"
    [items]="items"
    [selectAllButtonLabel]="'Select All'"
    [unselectAllButtonLabel]="'Unselect All'"
    [defaultToggleButtonLabel]="'No Items Selected'"
    [placeholder]="'Search Items'"
    [toggleBtnClass]="'btn-primary w-75'"
    [toggleContentClass]="'w-100'"
    [enableAnimation]="true"
    [useClassicCheckbox]="false"
    [enableResearch]="true"
    [disabled]="false"
></ngx-multiselect>
```

This is a simple interface that describes any parameters for a multiSelect component.

| Name                     | Type              | required | Description                                                                                                                                 | Default             |
| ------------------------ | ----------------- | :------: | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| (itemSelected)           | ItemSelectedEvent |    ✔️    | function who was called by the event for getting the list of selected items, in the example below the function was called getSelectedItem() | NO                  |
| items                    | item[]            |    ❌    | parameter item list                                                                                                                         | []                  |
| selectAllButtonLabel     | string            |    ❌    | button label for select all items                                                                                                           | 'Select All'        |
| unselectAllButtonLabel   | string            |    ❌    | button label for unselect all items                                                                                                         | 'Unselect All'      |
| defaultToggleButtonLabel | string            |    ❌    | label of toggle button in case of none items are selected                                                                                   | 'No Items Selected' |
| placeholder              | string            |    ❌    | placeholder of research input                                                                                                               | 'Search Items'      |
| toggleBtnClass           | string            |    ❌    | input for your custom css classes on the toggle button                                                                                      | 'btn-primary w-75'  |
| toggleContentClass       | string            |    ❌    | input for your custom css classes on the content of the toggle                                                                              | 'w-100'             |
| enableAnimation          | boolean           |    ❌    | enable or not the animation of the toggle content                                                                                           | true                |
| useClassicCheckbox       | boolean           |    ❌    | use simple font-awesome icon instead of animate checkbox                                                                                    | false               |
| enableResearch           | boolean           |    ❌    | display the research input                                                                                                                  | false               |
| disabled                 | boolean           |    ❌    | disable or not the toggle button                                                                                                            | false               |

In order to use the event class import it in your component and declare a new function in your component like this :

```typescript
    // import to be able to use the event
    import { ItemClickedEvent } from '@zokelion/ngx-multiselect/models/item-clicked-event.model';
    // import this model for the type of your list
    import { Item } from '@zokelion/ngx-multiselect/models/item.model';

    // function for getting and using the list
    public getSelectedItem(eventItem: ItemSelectedEvent): void {
        this.selectedItems = eventItem.selectedItems;
    }
```

For the generation of the tree the list must be composed of items based on this model :

```typescript
export class Item {
    id?: number;
    name: string;
    isSelected: boolean;
    children: Item[];
    cssClasses: string;
    cssSelectedClasse: string;
}
```

Detail of Item property :

| Name               | Type              | required | Description                                                 |
| ------------------ | ----------------- | :------: | ----------------------------------------------------------- |
| id                 | ItemSelectedEvent |    ❌    | item.id is optionnal but it is usefull when you use an api. |
| name               | string            |    ✔️    | name of item                                                |
| isSelected         | boolean           |    ✔️    | indicates weither or not this item is ticked.               |
| children           | item[]            |    ✔️    | childrens of the item                                       |
| cssClasses         | string            |    ✔️    | css classe(s) to use on your item                           |
| cssSelectedClasses | string            |    ✔️    | css classe(s) to use on your item when it's selected        |

Example of items list:

```typescript
// this list is an example
this.items.push({
    id: 1,
    name: 'World',
    isSelected: false,
    children: [
        {
            id: 2,
            name: 'America',
            isSelected: false,
            children: [
                {
                    id: 3,
                    name: 'Canada',
                    isSelected: false,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                },
                {
                    id: 4,
                    name: 'United-States',
                    isSelected: false,
                    children: [
                        {
                            id: 14,
                            name: 'Arizona',
                            isSelected: false,
                            children: [],
                            cssClasses: '',
                            cssSelectedClasses: 'bg-success text-light'
                        },
                        {
                            id: 15,
                            name: 'Washington',
                            isSelected: true,
                            children: [],
                            cssClasses: '',
                            cssSelectedClasses: 'bg-success text-light'
                        }
                    ],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                },
                {
                    id: 5,
                    name: 'Mexico',
                    isSelected: true,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                }
            ],
            cssClasses: '',
            cssSelectedClasses: 'bg-success text-light'
        },
        {
            id: 6,
            name: 'Europe',
            isSelected: true,
            children: [
                {
                    id: 7,
                    name: 'France',
                    isSelected: true,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                },
                {
                    id: 8,
                    name: 'Deutschland',
                    isSelected: true,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                }
            ],
            cssClasses: '',
            cssSelectedClasses: 'bg-success text-light'
        },
        {
            id: 9,
            name: 'Asia',
            isSelected: false,
            children: [
                {
                    id: 10,
                    name: 'China',
                    isSelected: false,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                },
                {
                    id: 11,
                    name: 'Japan',
                    isSelected: true,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                }
            ],
            cssClasses: '',
            cssSelectedClasses: 'bg-success text-light'
        },
        {
            id: 12,
            name: 'Oceania',
            isSelected: true,
            children: [
                {
                    id: 13,
                    name: 'Australia',
                    isSelected: true,
                    children: [],
                    cssClasses: '',
                    cssSelectedClasses: 'bg-success text-light'
                }
            ],
            cssClasses: '',
            cssSelectedClasses: 'bg-success text-light'
        }
    ],
    cssClasses: '',
    cssSelectedClasses: 'bg-success text-light'
});
```

### Configuration

Labels can be customized depending on your language. We're using English by default.
The labels of this components have default value but the following params can be customize :

```html
<ngx-multiselect
    [selectAllButtonLabel]="'Select All'"
    [unselectAllButtonLabel]="'Unselect All'"
    [defaultToggleButtonLabel]="'No Items Selected'"
    [placeholder]="'Search Items'"
    [toggleBtnClass]="'btn-primary w-75'"
    [toggleContentClass]="'w-100'"
    [enableAnimation]="true"
    [useClassicCheckbox]="false"
    [enableResearch]="true"
    [disabled]="false"
></ngx-multiselect>
```
