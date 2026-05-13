## Sub-menu: `/interface/ethernet/switch/qos/map` 

Priority-to-profile mapping table(-s) for trusted packets. All switch chips have one built-in map - default . In addition, some models allow the user to define custom mapping tables and assign different maps to various switch ports via the qos-map property: 

devices based on Marvell Prestera 98DX224S, 98DX226S , or 98DX3236 switch chip models support only one map - default. devices based on Marvell Prestera 98DX8xxx , 98DX4xxx switch chips, or 98DX325x model devices support up to 12 maps (the default + 11 userdefined). Property Description name (string; Default: ) The user-defined name of the mapping table.
