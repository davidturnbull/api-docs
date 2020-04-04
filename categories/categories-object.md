# Categories object

| **Attribute Name** |  | **Type** |  | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| **id** |  | number |  | The unique ID of the category. |
| **name** |  | string |  | The name of the category. Must be between 1 and 40 characters |
| **description** |  | string |  | A description of the category. Must not exceed 140 characters |
| **is\_income** |  | boolean |  | If `true`, the transactions in this category will be treated as income. |
| **exclude\_from\_budget** |  | boolean |  | If `true`, the transactions in this category will be excluded from the budget. |
| **exclude\_from\_totals** |  | boolean |  | If `true`, the transactions in this category will be excluded from totals. |
| **updated\_at** |  | string |  | The date and time of when the category was last updated (in the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) extended format). |
| **created\_at** |  | string |  | The date and time of when the category was created (in the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) extended format). |
| **is\_group** |  | boolean |  | If `true`, the category is treated as a group. |
| **group\_id** |  | number |  | The ID of a category group (or `null` if the category doesn't belong to a category group). |

