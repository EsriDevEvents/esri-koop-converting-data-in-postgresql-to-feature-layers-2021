# Esri Koop: Converting data in PostgreSQL to Feature Layers

Length: 30 min

Presenters: Raul Jimenez

Pre-recorded (On Demand)

## Summary

PostgreSQL is undoubtedly one of the most popular RDBMS, and although we can enable a PostgreSQL DB as a geodatabase it is not always possible. Therefore, in this session, we will learn how, thanks to Koop, we can enable the data of a PostgreSQL DB as ArcGIS Feature Layers. Keywords: ETL, Koop, RDBMS, Postgresql, Open source

## Demo script

```
# Install Koop-CLI if needed
npm install -g @koopjs/cli

koop new provider koop-provider-postgresql
cd koop-provider-postgresql
```

Provider code

```sql
SELECT St_asgeojson(St_transform(trees.geometry, 4326)),
    trees.*
FROM   trees,
    parks
WHERE  St_intersects(trees.geometry, parks.geometry)
    AND parks.name = 'Baker Park';
```



SELECT St_asgeojson(St_transform(P.geometry, 4326)), P.* FROM   parcels AS P INNER JOIN (SELECT parcel_id FROM   owners INNER JOIN owners_parcels ON owners.id = (SELECT id FROM   owners WHERE  email = 'raul.jimenez@esri.es' )) AS R ON P.parcel_id = R.parcel_id;
```sql
SELECT St_asgeojson(St_transform(P.geometry, 4326)),
       P.*
FROM   parcels AS P
       INNER JOIN (SELECT parcel_id
                   FROM   owners
                          INNER JOIN owners_parcels
                                  ON owners.id = (SELECT id
                                                  FROM   owners
                                                  WHERE  email =
                                                 'raul.jimenez@esri.es'
                                                 )) AS R
               ON P.parcel_id = R.parcel_id; 
```

```
koop serve --debug
```
