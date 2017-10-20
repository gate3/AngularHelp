# Expression Changed After View Was Checked

> **ERROR Error: ExpressionChangedAfterItHasBeenCheckedError: Expression has changed after it was checked.**

This error occurs in dev mode. You can see that it doesn't occur in production mode by calling enableProdMode(). The reason it occurs is that after every round of change detection, dev mode immediately performs a second round to verify that no bindings have changed since the end of the first, as this would indicate that changes are being caused by change detection itself.

## Solution 

You need to explicitly fire change detection yourself to inform angular that there has been a change. Sample code below

```typescript 

import {ChangeDetectorRef} from '@angular/core'

...
pageLoaded:boolean = false

constructor (private cdRef:ChangeDetectorRef) {}

ngAfterViewInit(): void {
    this.pageLoaded = true

    //call detectChanges immediately after the change causing the error
    this.cdRef.detectChanges();
}

...
...

```