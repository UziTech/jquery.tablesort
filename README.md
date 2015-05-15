# jquery.tablesort
Simple jQuery plugin for sorting table rows
# Usage
#### Include the plugin
```html
<script src="/path/to/jquery.tablesort.js"></script>
```
#### Add class="sortable" to any sortable columns along with a data-sorttype attribute if you want it to sort by something other than string.
```html
<table>
  <thead>
    <tr>
      <th>not sortable</th>
      <th class="sortable" data-sorttype="number">number</th>
      <th class="sortable">string</th>
      <th class="sortable" data-sorttype="date">date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>this</td>
      <td>1</td>
      <td>a</td>
      <td>2/3/2015</td>
    </tr>
    <tr>
      <td>column is</td>
      <td>2</td>
      <td>c</td>
      <td>3/4/15</td>
    </tr>
    <tr>
      <td>not sortable</td>
      <td>3</td>
      <td>b</td>
      <td>2015-01-01</td>
    </tr>
  </tbody>
</table>
```
#### Call the plugin on the table.
```javascript
$("table").tablesort();
```
## More Options
#### Create custom sort.
create a custom sorttype to sort date range by first date

|   date range    |
-------------------
|5/17/15 - 5/23/15|
|5/10/15 - 5/16/15|
|5/03/15 - 5/09/15|
|4/26/15 - 5/02/15|
|4/19/15 - 5/25/15|

```html
      <th class="sortable" data-sorttype="date-range">date range</th>
```
```javascript
$("table").tablesort({
	sorttypes: {
		"date-range": function (a, b) {
			var am = a.match(/^\d+\/\d+\/\d+/);
			var bm = b.match(/^\d+\/\d+\/\d+/);
			if (am === null || bm === null) {
				return 0;
			}
			var av = new Date(am[0]);
			var bv = new Date(bm[0]);
			if (av < bv) {
				return -1;
			} else if (av > bv) {
				return 1;
			} else {
				return 0;
			}
		}
	}
});
```
