# CodingTipsAndTricks
Tips and tricks when coding

## Clear coding
Write your code such that it is easier for yourself and others to read.

Example:
```js
// hard to understand
        if (e.sender.dataSource.total() === 1) {
            e.sender.expandRow(".k-master-row");
        }
        
// easier to understand
        var weHaveOnlyOneRow = e.sender.dataSource.total() === 1;
        var expandRows = function expandRows() { e.sender.expandRow(".k-master-row"); };

        if (weHaveOnlyOneRow) {
            expandRows();
        }
```

Move complex or unclear expressions into named functions or variables. The more carefully you craft your names, the easier it is to understand what you intend to do. Both for others and yourself when you come back two months later.
