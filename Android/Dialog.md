> Thinking

```
Dialog
    AlertDialog
        ProgressDialog
        DatePickerDialog
        TimePickerDialog
```

> Memory

```
Dialog dialog = new Dialog(context);
dialog.cancel(); dialog.setOnCancelListener(new DialogInterface.OnCancelListener() {
    @Override
    public void onCancel(DialogInterface dialogInterface) { }
});
dialog.dismiss(); dialog.setOnDismissListener(new DialogInterface.OnDismissListener() {
    @Override
    public void onDismiss(DialogInterface dialogInterface) { }
});
dialog.show(); dialog.isShowing(); dialog.setOnShowListener(new DialogInterface.OnShowListener() {
    @Override
    public void onShow(DialogInterface dialogInterface) { }
});
dialog.setOnKeyListener(new DialogInterface.OnKeyListener() {
    @Override
    public boolean onKey(DialogInterface dialogInterface, int i, KeyEvent keyEvent) { return false; }
});
dialog.setCancelable(false); dialog.setCanceledOnTouchOutside(true);
dialog.hide();

ProgressDialog progressDialog = new ProgressDialog(this);
progressDialog.setTitle("");
progressDialog.setMessage("");
progressDialog.setIndeterminate(true);
progressDialog.setCancelable(false);
progressDialog.setOnCancelListener(new DialogInterface.OnCancelListener() {
    @Override
    public void onCancel(DialogInterface dialogInterface) { }
});
progressDialog.show();

new AlertDialog.Builder(context)
        .setIcon(R.drawable.ic_launcher_background)
        .setTitle("")
        .setMessage("")
        .setPositiveButton("", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) { }
        })
        .setNegativeButton("", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) { }
        })
        .setNeutralButton("", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) { }
        })
        .show();

AlertDialog alertDialog = new AlertDialog.Builder(this)
        .setCancelable(false).create();
alertDialog.show();
alertDialog.getWindow().setContentView(new View(this));
alertDialog.getWindow().findViewById(R.id.accelerate);

```

