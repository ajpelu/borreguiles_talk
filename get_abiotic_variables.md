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


CREATE TABLE aux_ajpelu_bor_cli as

SELECT 
 v.cli_id,
 cli_celdas.id,
 cli_mapas_pasados.cli_celda_id,
 cli_indice_mapas_pasados.ano, 
 cli_variables.codigo, 
 cli_variables.descripcion, 
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
  cli_indice_mapas_pasados.cli_variable_id = cli_variables.id LIMIT 10;
  
  
  
  
 
 SELECT 
  aux_ajpelu_cli.cli_id, 
  cli_celdas.id, 
  aux_ajpelu_cli.pob, 
  cli_celdas.the_geom
FROM 
  public.aux_ajpelu_cli, 
  public.cli_celdas
WHERE 
  aux_ajpelu_cli.cli_id = cli_celdas.id;
 
 
 
