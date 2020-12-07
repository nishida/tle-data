# tle-data

[`create_daily_data.ipynb`](https://github.com/nishida/tle/blob/main/create_daily_data.ipynb) で生成したデータファイル。

## [5d80dc1](https://github.com/nishida/tle-data/commit/5d80dc18c635c1118c74357f7e6037e7b6127da7) (2020年12月7日)での計算方法

1. 軌道長半径、近地点高度、遠地点高度を算出する。
```
df['SEMIMAJOR_AXIS'] = (398600.4418 / (df['MEAN_MOTION'] * 2 * math.pi / (24 * 3600)) ** 2) ** (1/3)
df['APOAPSIS'] = (df['SEMIMAJOR_AXIS'] * (1 + df['ECCENTRICITY']))- 6378.135
df['PERIAPSIS'] = (df['SEMIMAJOR_AXIS'] * (1 - df['ECCENTRICITY']))- 6378.135
```
2. 毎日0:00UT時点での値を前後の値から線形補間により求める。
3. 日変化を計算する。
