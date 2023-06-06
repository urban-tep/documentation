# Test data

The Urban TEP processor development VM comes with a few Earth observation products from different missions and sensors:

- Sentinel 2 L1C subset
- Landsat 8 OLI+TIRS
- ENVISAT MERIS

The test data is located in directory /urbantep/eodata/\<type> in the virtual machine:

```
urbanuser@urbandev:~ $ tree /urbantep/eodata
/urbantep/eodata
├── LC8
│   └── v1
│       └── 2014
│           └── 07
│               └── 03
│                   └── LC81940272014184LGN00.tar.gz
├── MER_FSG_1P
│   └── v2013
│       └── 2009
│           └── 06
│               └── 01
│                   └── MER_FSG_1PPEPA20090601_112030_000004532079_00295_37924_7073.N1
└── S2_L1C
    └── v1
        └── 2015
            └── 12
                └── 17
                    └── S2A_OPER_PRD_MSIL1C_PDMC_20151217T195044_R108_V20151217T103953_20151217T103953-Lake-Constance-UTM32N.nc
```

Additional test data can be added by downloading it from the respective provider's data gateways, e.g. Copernicus Sentinel Data Hub for Sentinel-2 or USGS EarthExplorer for Landsat-8.
