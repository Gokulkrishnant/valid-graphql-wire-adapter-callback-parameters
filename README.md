# Lightning Web Component (LWC) Wire Function Example

This example demonstrates the correct usage of the wire function in a Lightning Web Component. The wire function should use either a wire property or a wire function callback to handle the result and data, but not both.

## Incorrect Implementation

In this example, the wire service improperly uses both a wire property and a wire function callback for the same method, which is not allowed.

```javascript
// myComponent.js (Incorrect)
import { LightningElement, wire } from 'lwc';
import getAccountList from '@salesforce/apex/AccountController.getAccountList';

export default class MyComponent extends LightningElement {
    @wire(getAccountList) accounts; // Wire property
    
    @wire(getAccountList)
    wiredAccounts({ error, data }) { // Wire function callback
        if (data) {
            console.log('Accounts data:', data);
        } else if (error) {
            console.error('Error fetching accounts:', error);
        }
    }
}
```
# Lightning Web Component (LWC) Wire Function Example

This example demonstrates the corrected usage of the wire function in a Lightning Web Component, focusing on using the wire function callback appropriately.

## Corrected Implementation

In this corrected example, the code uses only the wire function callback to handle the result of the `getAccountList` method from the Apex controller. This approach provides more control and ensures proper handling of both data and error states.

```javascript
// myComponent.js (Corrected)
import { LightningElement, wire, track } from 'lwc';
import getAccountList from '@salesforce/apex/AccountController.getAccountList';

export default class MyComponent extends LightningElement {
    @track accounts;
    @track error;

    // Using wire function callback to fetch account data
    @wire(getAccountList)
    wiredAccounts({ error, data }) {
        if (data) {
            this.accounts = data;
            this.error = undefined;
        } else if (error) {
            this.error = error;
            this.accounts = undefined;
        }
    }
}
```
