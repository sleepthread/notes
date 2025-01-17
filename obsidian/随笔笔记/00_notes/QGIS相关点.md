
1、12-23
```python
# 经过测试，intersection是矩阵的相交，也就是两个矩阵中相同列提取出来  
# gdp_area_pop_intersection_layer = gdp_area_layer.intersection(gdp_pop_layer)



gpd_area_layer = gpd.read_file(layer_file_path, layer=layer_name)  
if gpd_area_layer.empty:  
    continue  
gpd_flood_layer = gpd.read_file(flood_hazard_file_path, layer=flood_hazard_checked_layer.sourceName())  
  
# 打印当前 CRSprint("Original CRS-gpd_area_layer:", gpd_area_layer.crs)  
print("Original CRS-gpd_flood_layer:", gpd_flood_layer.crs)  
gpd_area_layer = gpd_area_layer.to_crs(epsg=32650)  
gpd_flood_layer = gpd_flood_layer.to_crs(epsg=32650)  
print("Original CRS-gpd_area_layer-1:", gpd_area_layer.crs)  
print("Original CRS-gpd_flood_layer-1:", gpd_flood_layer.crs)  
  
# 计算数据1中去掉数据2交集部分，保留的geometry为数据1去掉后的部分  
gpd_area_impact_layer = gpd.overlay(gpd_area_layer, gpd_flood_layer, 'intersection')





# 获取人口图层的几何类型  
pop_layer_wkb_type = pop_layer_source.wkbType()  
# print('pop_layer_wkb_type', pop_layer_wkb_type)  
# print('QgsWkbTypes.PointGeometry', QgsWkbTypes.PointGeometry)  
# print('QgsWkbTypes.LineGeometry', QgsWkbTypes.LineGeometry)  
# print('QgsWkbTypes.PolygonGeometry ', QgsWkbTypes.PolygonGeometry)  
# print('Qgis.WkbType.Point ', Qgis.WkbType.Point)  
# print('Qgis.WkbType.MultiPoint ', Qgis.WkbType.MultiPoint)  
# print('Qgis.WkbType.LineString ', Qgis.WkbType.LineString)  
# print('Qgis.WkbType.MultiLineString ', Qgis.WkbType.MultiLineString)  
# print('Qgis.WkbType.Polygon ', Qgis.WkbType.Polygon)  
# print('Qgis.WkbType.MultiPolygon ', Qgis.WkbType.MultiPolygon)  
  
point_type_list = [Qgis.WkbType.Point, Qgis.WkbType.MultiPoint]  
line_type_list = [Qgis.WkbType.LineString, Qgis.WkbType.MultiLineString]  
polygon_type_list = [Qgis.WkbType.Polygon, Qgis.WkbType.MultiPolygon]


```





2、