# Macrometa MetaFlix

A geo-distributed Netflix clone running at the edge with low latency & superior experience to users.


## Setup

| **Federation**                                        | **Email**                              | **Passsword** | **Dashboard**|
| ----------------------------------------------------- | -------------------------------------- | ------------- |--------------|
| [Global Data Network](https://gdn.paas.macrometa.io/) | demo-ott-app@macrometa.io | `xxxxxxxx`    | [Dashboard](https://macrometacorp.github.io/metaflix-fastly/) |



## Solution

1. Create the following collections in your GDN account:

```
assets (global)
genres (global)
credits (global)
my_list (global)
users (global)
asset_credit_edge (graph-edge, global)
genres_asset_edge (graph-edge, local)
```

2. Create the following search views in your GDN account:

**`asset_credit_view`** with Primary sort field `popularity`

| **Mapping - Collection** | **Field** | **Analyzer** |
| ------------------------ | --------- | ------------- |
| assets | title | text_en |
| assets | original_title | text_en |
| assets | overview | text_en |
| credits | name | text_en |

**`asset_type_view`**

| **Mapping - Collection** | **Field** | **Analyzer** |
| ------------------------ | --------- | ------------- |
| genres_asset_edge | asset_type | identity |

3. Create the following graph in your federation:

**`OTT`**

| **Edge Definitions** | **From Collections** | **To Collections** |
| ------------------------ | --------- | ------------- |
| genres_asset_edge | genres | assets |
| asset_credit_edge | assets | credits |

4. Create the following Query workers in your GDN Account:

```
getMovieAssetsByGenre
getTopRatedMovies
getTopRatedTvSeries
getTvSeriesAssetsByGenre
searchByAsset
searchByCredits
```

**GitHub** - https://github.com/Macrometacorp/metaflix-fastly
