```
CREATE TABLE `ses_delivery` (
    `messageid` varchar(60) COLLATE latin1_general_cs NOT NULL DEFAULT '',
  `delivered_at` timestamp NULL DEFAULT NULL,
  PRIMARY KEY (`messageid`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_general_cs;
```

```
CREATE TABLE `ses_open` (
    `messageid` varchar(60) COLLATE latin1_general_cs NOT NULL DEFAULT '',
  `opened_at` timestamp NULL DEFAULT NULL,
  PRIMARY KEY (`messageid`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_general_cs;
```

```
CREATE TABLE `ses_click` (
    `messageid` varchar(60) COLLATE latin1_general_cs NOT NULL DEFAULT '',
  `clicked_at` timestamp NULL DEFAULT NULL,
  `click_count` int(10) NULL DEFAULT NULL,
  PRIMARY KEY (`messageid`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_general_cs;
```