### Abiotic information

We obtain information about abiotics variables that could be related with phenology of borreguiles. 

#### Climatic information 

First we obtain information from climatics maps for pixels over 2300 m. 

##### Spatial information
* Select the elevation over 2300 m. 
* Load `/Volumes/cartografia/Informacion_Ambiental/CARTO_TEMATICA/Medio_biofisico/Relieve/vectorial/curvas_snevada.shp` shapefile.
* Spatial Query: `"CONTOUR" = 2300` 
* Export layer as: `./geoinfo/2300_line.shp` 
* Edit and clear the 2300_line:
 * Select only the greater polygon
 * Close the greater polygon
 * Remove small parts 
 * Save it as `./geoinfo/2300_clear_pol.shp`
* Import it into linaria: 


SELECT UpdateGeometrySRID('aux_ajpelu_2300','geom',23030);




SELECT 
 cli_celdas.id as cli_celda_id,
 cli_indice_mapas_pasados.ano, 
 cli_variables.codigo, 
 cli_mapas_pasados.valor
FROM
  cli_celdas, 
  (SELECT 
    cli_celdas.id as cli_id
  FROM 
    aux_ajpelu_2300 as aux, 
    cli_celdas
  WHERE 
    ST_Within(cli_celdas.the_geom, aux.geom)) AS v,
  cli_mapas_pasados,
  cli_indice_mapas_pasados,
  cli_variables
WHERE 
  v.cli_id = cli_celdas.id AND
  v.cli_id = cli_mapas_pasados.cli_celda_id AND
  cli_mapas_pasados.cli_indice_mapas_pasado_id = cli_indice_mapas_pasados.id AND
  cli_indice_mapas_pasados.cli_variable_id = cli_variables.id;
  
  
  
  
  
  
 
 
CREATE TABLE aux_ajpelu_cli_celdas2300 AS
SELECT 
    cli_celdas.id as cli_id,
    cli_celdas.the_geom
  FROM 
    aux_ajpelu_2300 as aux, 
    cli_celdas
  WHERE 
    ST_Within(cli_celdas.the_geom, aux.geom);


##### NIEVE 
* See distribution of borreguiles plots
* See San Juan basin (J. Herrero)
* Get the id of pixels of the SanJuan basin
```
c(1671139,1671140,1671141,1671142,1671143,1671144,1671145,1671146,1671147,1671148,1673541,1673542,1673543,1673544,1673545,1673546,1673547,1673548,1673549,1673550,1675943,1675944,1675945,1675946,1675947,1675948,1675949,1675950,1675951,1675952,1678345,1678346,1678347,1678348,1678349,1678350,1678351,1678352,1678353,1678354,1680747,1680748,1680749,1680750,1680751,1680752,1680753,1680754,1680755,1680756,1683149,1683150,1683151,1683152,1683153,1683154,1683155,1683156,1683157,1683158,1685551,1685552,1685553,1685554,1685555,1685556,1685557,1685558,1685559,1685560,1687953,1687954,1687955,1687956,1687957,1687958,1687959,1687960,1687961,1687962,1690355,1690356,1690357,1690358,1690359,1690360,1690361,1690362,1690363,1690364,1692757,1692758,1692759,1692760,1692761,1692762,1692763,1692764,1692765,1692766,1695159,1695160,1695161,1695162,1695163,1695164,1695165,1695166,1695167,1695168,1697561,1697562,1697563,1697564,1697565,1697566,1697567,1697568,1697569,1697570)
```









  
 
