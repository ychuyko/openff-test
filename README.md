# Тестовое задание в группу Вычислительной химии BIOCAD
В качестве задания мной была выбрана задача параметризации большого количества малых молекул полем OpenFF. Мной был написан [Jupyter-notebook](./openff.ipynb), который выполняется в
в [Conda-окружении](./environment.yml). 

* 1. Создание окружения
```
conda env create -f environment.yml
conda activate openff-toolkit
python -m ipykernel install --user --name=openff-toolkit
```
* 2. Jupyter-notebook работает в созданном окружении (мы его добавили в kernel). Входной файл `example.sdf` загружается в созданную директорию `data`. А
     нужные файлы структур и топологий создаются в директории `gro_files`, каждая молекула в отдельной папке, названной именем молекулы CHEMBL*.\
     Комментарии по заданию:
     * Для обработки одной молекулы требуется в среднем ~1 минута на локальном компьютере, больше всего времени занимает создание объекта Interchange, который необходим для
       конвертации в .gro и .top файлы. Потребление ресурсов при выполнении этой команды требует оптимизации, так как она выполняется на одном CPU.
     * Расчет частичных зарядов производится в силовом поле Sage с помощью AM1/BCC. На мой взгляд можно воспользоваться [PsiRESP](https://psiresp.readthedocs.io/en/latest/), как более
       точным методом. Для этого потребуются дополнительные манипуляции с файлом топологии.
     * Требованием к заданию было сохранение координат атомов, как во входном файле .sdf. В полученных GRO файлах координаты сохранены в нанометрах. В sdf файле коордианты записаны в ангстремах,
       а при создании объекта Interchange используются единицы измерения по умолчанию - нанометры. Это можно изменить с помощью пакета `openff-units`, но при выполнении функции `.to_gromacs`
       ангстремы все равно переводятся в нанометры, но для GRO файлов это единица измерения по умолчанию.

