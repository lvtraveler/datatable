# datatable
使用datatable加载json数据，并给datatable添加checkbox全选操作


## 操作

引入js:

```

- <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
-	<script type="text/javascript" src="http://cdn.datatables.net/s/dt/dt-1.10.10,se-1.1.0/datatables.min.js"></script>
-	<script type="text/javascript" src="http://gyrocode.github.io/jquery-datatables-checkboxes/1.0.1/js/dataTables.checkboxes.min.js"></script>

```

引入css:

```

- <link rel="stylesheet" type="text/css" href="http://cdn.datatables.net/s/dt/dt-1.10.10,se-1.1.0/datatables.min.css">
-	<link rel="stylesheet" type="text/css" href="http://gyrocode.github.io/jquery-datatables-checkboxes/1.0.1/css/dataTables.checkboxes.css">

```

配置datatable:

```
$(document).ready(function (){
   var table = $('#example').DataTable({
      'ajax': './demo.json',
      'columns':[
      	{"data":"input"},
      	{"data":"name"},
    	{"data":"desc"},
    	{"data":"url"},
    	{"data":"way"},
    	{"data":"result"},
    	{"data":"details"}
      ],
      'columnDefs': [
         {
            'targets': 0,
            'checkboxes': {
               'selectRow': true
            }
         }
      ],
      'select': {
         'style': 'multi'
      },
      'order': [[1, 'asc']]
   });


   // Handle form submission event 
   $('#frm-example').on('submit', function(e){
      var form = this;
      
      var rows_selected = table.column(0).checkboxes.selected();

      // Iterate over all selected checkboxes
      $.each(rows_selected, function(index, rowId){
         // Create a hidden element 
         $(form).append(
             $('<input>')
                .attr('type', 'hidden')
                .attr('name', 'id[]')
                .val(rowId)
         );
      });
   });
});

```

**注意:**

```

'columns':[
      	{"data":"input"},
      	{"data":"name"},
    	{"data":"desc"},
    	{"data":"url"},
    	{"data":"way"},
    	{"data":"result"},
    	{"data":"details"}
      ],

```      
这项配置必须和你的json文件中的键名在名字上和数量上保持一致，否则datatable.js会报错！
