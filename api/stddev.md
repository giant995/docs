---
api_name: stddev() | stddev_y() | stddev_x()
excerpt: Calculate the standard deviation from values in a statistical aggregate
topics: [hyperfunctions]
keywords: [statistics, statistical aggregate, hyperfunctions, toolkit]
tags: [standard deviation]
api:
  license: community
  type: function
  toolkit: true
hyperfunction:
  family: statistical aggregates
  type: accessor, 1D
  aggregates:
    - stats_agg()
# fields below will be deprecated
api_category: hyperfunction
toolkit: true
hyperfunction_family: 'statistical aggregates'
hyperfunction_subfamily: 'statistical aggregates'
hyperfunction_type: accessor-1d
---

# stddev() / stddev_y() / stddev_x() <tag type="toolkit">Toolkit</tag>

```SQL
stddev(summary StatsSummary1D, method TEXT) RETURNS BIGINT
```

```SQL
stddev_y(summary StatsSummary2D, method TEXT) RETURNS BIGINT
```

```SQL
stddev_x(summary StatsSummary2D, method TEXT) RETURNS BIGINT
```

Get the standard deviation of the values contained in a statistical aggregate.
In a two-dimensional [`stats_agg`][stats-agg] use the `_y`/ `_x` form to access the
`stddev` of the dependent and independent variables.

The `method` determines whether you calculate a 'population' or 'sample' standard deviation.
These values may be provided as their full names or may be abbreviated 'pop' or 'samp'. These
are the only four accepted values for the `method` argument. The default is 'sample'.

For more information about statistical aggregate functions, see the
[hyperfunctions documentation][hyperfunctions-stats-agg].

## Required arguments

|Name|Type|Description|
|-|-|-|
|`summary`|`StatsSummary1D`/`StatsSummary2D`|The already constructed data structure from a previous [`stats_agg`][stats-agg] call|

### Optional arguments

|Name|Type|Description|
|-|-|-|
|`method`|`TEXT`|The method for the calculation 'population' or 'sample' (default)|

## Returns

|Column|Type|Description|
|-|-|-|
|`stddev`/`stddev_y`/`stddev_x`|`DOUBLE PRECISION`|The standard deviation of the values in the statistical aggregate|

## Sample usage

```SQL
SELECT stddev_y(stats_agg(data, data))
FROM generate_series(0, 100) data;
```

```output
 stddev_y 
----------
  29.3002
```

[hyperfunctions-stats-agg]: /timescaledb/:currentVersion:/how-to-guides/hyperfunctions/stats-aggs/
[stats-agg]: /api/:currentVersion:/hyperfunctions/stats_aggs/stats_agg/
