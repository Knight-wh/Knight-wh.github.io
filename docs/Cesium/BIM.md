# BIM数据结构笔记

> Revit和IFC使用的是以固定坐标定位数据的三维笛卡尔坐标系。BIM坐标本质上不是地理位置，而是相对于几何原点(0,0,0)的位置。

## Revit文件坐标

## IFC文件坐标

可以在 IFC 文件中使用与定义的地理空间坐标系相应的线性单位和坐标值创建几何坐标系。 如果此坐标系的对应项包括 PRJ 文件，则数据会在 ArcGIS Pro 中正确定位。

与其他 CAD 和 BIM 数据一样，如果文件坐标未对应于分配的坐标系 (PRJ) 的坐标，则必须创建包含所需坐标变换的坐标定位文件，或包括它以正确定位数据。 使用为地理配准 BIM 数据提供的工具生成坐标定位文件。

## IFC scheme

IFCscheme中有几种属性properties，每一种属性都有特殊的用处。

- Native properties. 每个IFC类的规格。
- Type properties. 描述相同类型的所有元素的属性。
- Material properties. 描述组成这个元素的层次的所有材质。
- Property sets. 用户定义的属性的集合。
- Quantity sets. Sets of properties describing the dimensions of the elements to which they refer.

