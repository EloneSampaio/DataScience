```python
import pandas as pd
import numpy as np
from faker import Faker
from faker_airtravel import AirTravelProvider
from datetime import datetime
from random import randrange
import random

```


```python

```

### váriaveis


```python
fcompras = []
dfornecedor = []
dcomprador = []
dmateriaprima = []
fcustopadrao = []
n = 1000
```


```python
fake = Faker('pt_BR')
fake.add_provider(AirTravelProvider)
```

# Criar tabela dFornecedor


```python
for n in range(n):
    
    idFornecedor =fake.unique.pyint()
    fornecedor = fake.name_nonbinary()
    PrazoEntregaPadrao = randrange(20)
    dfornecedor.append([idFornecedor,fornecedor,PrazoEntregaPadrao])
dataFrame_dfornecedor = pd.DataFrame(dfornecedor,columns=['idFornecedor','fornecedor','PrazoEntregaPadrao'])
```


```python

```

# Criar tabela dComprador


```python
for n in range(n):
    
    idComprador =fake.unique.pyint()
    comprador = fake.name_nonbinary()
  
    dcomprador.append([idComprador,comprador])
dataFrame_dcomprador = pd.DataFrame(dcomprador,columns=['idComprador','comprador'])
```


```python

```

# Criar tabela dMateriaPrima


```python
for n in range(n):
    
    idMateriaPrima = fake.unique.pyint()
    materiaPrima = fake.airport_iata()
    
    dmateriaprima.append([idMateriaPrima,materiaPrima])
dataFrame_dmateriaprima = pd.DataFrame(dmateriaprima,columns=['idMateriaPrima','materiaPrima'])
```


```python

```


```python

```


```python

```

## Criar tabela fcompras


```python

```


```python

```


```python
for m in range(n):
    
    d1 = datetime.strptime(f'01/01/2021','%d/%m/%Y')
    d2 = datetime.strptime(f'29/06/2021','%d/%m/%Y')
    
    d3 = datetime.strptime(f'30/06/2021','%d/%m/%Y')
    d4 = datetime.strptime(f'30/08/2021','%d/%m/%Y')

    d5 = datetime.strptime(f'01/09/2021','%d/%m/%Y')
    d6 = datetime.strptime(f'05/11/2021','%d/%m/%Y')
    
    idRequisicao = fake.unique.isbn10()
    dataRequisicao = fake.date_between(d1,d2)
    dataSaida = fake.date_between(d3,d4)
    dataEntrega = fake.date_between(d5,d6)
    
    #idComprador = fake.unique.isbn10()
    #comprador = fake.name()
    
    #idMateriaPrima = fake.unique.isbn10()
    #materiaPrima = fake.airport_iata()
    
    #idFornecedor =fake.unique.isbn10()
    #fornecedor = fake.name_nonbinary()
    
    #prazodeEntregaFornecedor = randrange(20)
    TemContrato=random.choice(['Sim','Não'])
    
    quantidade= randrange(20)
    custoUnitario=fake.pyfloat(right_digits=2,positive=True,min_value=500,max_value=1000)
    ValorTotal= custoUnitario * quantidade
    
    fcompras.append([idRequisicao,dataRequisicao,dataSaida,dataEntrega,TemContrato,quantidade,custoUnitario,ValorTotal])
dataFramefcompras =  pd.DataFrame(fcompras,columns=['idRequisicao','dataRequisicao','dataSaida','dataEntrega',
                                                    'TemContrato','quantidade','custoUnitario','ValorTotal'
                    ])   
```


```python
dataFramefcompras['idComprador'] = dataFrame_dcomprador['idComprador']
dataFramefcompras['idFornecedor'] = dataFrame_dfornecedor['idFornecedor']
dataFramefcompras['idMateriaPrima'] = dataFrame_dmateriaprima['idMateriaPrima']
dataFramefcompras['DataPrevistaEntrega']= pd.to_datetime(dataFramefcompras.dataSaida) + pd.to_timedelta(pd.np.ceil(dataFrame_dfornecedor.PrazoEntregaPadrao),unit="D")
```

    <ipython-input-363-3a784b822f3f>:4: FutureWarning: The pandas.np module is deprecated and will be removed from pandas in a future version. Import numpy directly instead
      dataFramefcompras['DataPrevistaEntrega']= pd.to_datetime(dataFramefcompras.dataSaida) + pd.to_timedelta(pd.np.ceil(dataFrame_dfornecedor.PrazoEntregaPadrao),unit="D")



```python
dataFramefcompras.head()
```




<div><div id=c4d8da1e-c8ce-4935-831e-7da536b965b6 style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('c4d8da1e-c8ce-4935-831e-7da536b965b6').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idRequisicao</th>
      <th>dataRequisicao</th>
      <th>dataSaida</th>
      <th>dataEntrega</th>
      <th>TemContrato</th>
      <th>quantidade</th>
      <th>custoUnitario</th>
      <th>ValorTotal</th>
      <th>idComprador</th>
      <th>idFornecedor</th>
      <th>idMateriaPrima</th>
      <th>DataPrevistaEntrega</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-120-54579-X</td>
      <td>2021-05-18</td>
      <td>2021-07-18</td>
      <td>2021-09-17</td>
      <td>Sim</td>
      <td>4</td>
      <td>926.36</td>
      <td>3705.44</td>
      <td>4314</td>
      <td>5619</td>
      <td>7203</td>
      <td>2021-07-28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0-85512-018-5</td>
      <td>2021-03-23</td>
      <td>2021-08-17</td>
      <td>2021-09-10</td>
      <td>Sim</td>
      <td>19</td>
      <td>832.18</td>
      <td>15811.42</td>
      <td>7288</td>
      <td>6688</td>
      <td>3828</td>
      <td>2021-09-05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0-85452-746-X</td>
      <td>2021-01-02</td>
      <td>2021-07-27</td>
      <td>2021-09-28</td>
      <td>Não</td>
      <td>13</td>
      <td>722.32</td>
      <td>9390.16</td>
      <td>389</td>
      <td>5904</td>
      <td>5329</td>
      <td>2021-07-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1-59815-702-7</td>
      <td>2021-03-28</td>
      <td>2021-07-25</td>
      <td>2021-09-06</td>
      <td>Sim</td>
      <td>6</td>
      <td>747.75</td>
      <td>4486.50</td>
      <td>2640</td>
      <td>1292</td>
      <td>6018</td>
      <td>2021-08-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0-264-87742-X</td>
      <td>2021-06-17</td>
      <td>2021-08-28</td>
      <td>2021-10-18</td>
      <td>Sim</td>
      <td>3</td>
      <td>568.79</td>
      <td>1706.37</td>
      <td>331</td>
      <td>2879</td>
      <td>9128</td>
      <td>2021-09-07</td>
    </tr>
  </tbody>
</table></div>



# Criar tabela fCustosPadrão


```python

```


```python
dataFramefcompras.head()
```




<div><div id=5e201e3e-2fec-4101-bda6-d6e2988ab528 style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('5e201e3e-2fec-4101-bda6-d6e2988ab528').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idRequisicao</th>
      <th>dataRequisicao</th>
      <th>dataSaida</th>
      <th>dataEntrega</th>
      <th>TemContrato</th>
      <th>quantidade</th>
      <th>custoUnitario</th>
      <th>ValorTotal</th>
      <th>idComprador</th>
      <th>idFornecedor</th>
      <th>idMateriaPrima</th>
      <th>DataPrevistaEntrega</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-120-54579-X</td>
      <td>2021-05-18</td>
      <td>2021-07-18</td>
      <td>2021-09-17</td>
      <td>Sim</td>
      <td>4</td>
      <td>926.36</td>
      <td>3705.44</td>
      <td>4314</td>
      <td>5619</td>
      <td>7203</td>
      <td>2021-07-28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0-85512-018-5</td>
      <td>2021-03-23</td>
      <td>2021-08-17</td>
      <td>2021-09-10</td>
      <td>Sim</td>
      <td>19</td>
      <td>832.18</td>
      <td>15811.42</td>
      <td>7288</td>
      <td>6688</td>
      <td>3828</td>
      <td>2021-09-05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0-85452-746-X</td>
      <td>2021-01-02</td>
      <td>2021-07-27</td>
      <td>2021-09-28</td>
      <td>Não</td>
      <td>13</td>
      <td>722.32</td>
      <td>9390.16</td>
      <td>389</td>
      <td>5904</td>
      <td>5329</td>
      <td>2021-07-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1-59815-702-7</td>
      <td>2021-03-28</td>
      <td>2021-07-25</td>
      <td>2021-09-06</td>
      <td>Sim</td>
      <td>6</td>
      <td>747.75</td>
      <td>4486.50</td>
      <td>2640</td>
      <td>1292</td>
      <td>6018</td>
      <td>2021-08-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0-264-87742-X</td>
      <td>2021-06-17</td>
      <td>2021-08-28</td>
      <td>2021-10-18</td>
      <td>Sim</td>
      <td>3</td>
      <td>568.79</td>
      <td>1706.37</td>
      <td>331</td>
      <td>2879</td>
      <td>9128</td>
      <td>2021-09-07</td>
    </tr>
  </tbody>
</table></div>




```python
dataFramfcustopadrao = pd.DataFrame(columns=['idMateriaPrima','idFornecedor','custoUnitarioPadrao'])
```


```python
dataFramfcustopadrao['idMateriaPrima']=dataFramefcompras['idMateriaPrima']
dataFramfcustopadrao['idFornecedor']=dataFramefcompras['idFornecedor']


```


```python
custoUnitarioPadrao = []
```


```python
for n in range(n):
    dataValor=fake.pyfloat(right_digits=2,positive=True,min_value=1,max_value=500,)
    
    custoUnitarioPadrao.append(dataValor)


```


```python
dataFramfcustopadrao['custoUnitarioPadrao'] = custoUnitarioPadrao
```


```python

```


```python
dataFramfcustopadrao.head()
```




<div><div id=694b71fe-faff-41d6-bc38-be9cf5c21deb style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('694b71fe-faff-41d6-bc38-be9cf5c21deb').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idMateriaPrima</th>
      <th>idFornecedor</th>
      <th>custoUnitarioPadrao</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7203</td>
      <td>5619</td>
      <td>458.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3828</td>
      <td>6688</td>
      <td>108.40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5329</td>
      <td>5904</td>
      <td>433.77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6018</td>
      <td>1292</td>
      <td>434.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9128</td>
      <td>2879</td>
      <td>181.42</td>
    </tr>
  </tbody>
</table></div>




```python

```

# Exportar dados


```python
dataFramefcompras.to_excel('fcompras.xlsx',index=False)
dataFramfcustopadrao.to_excel('fcustopadrao.xlsx',index=False)
dataFrame_dfornecedor.to_excel('dfornecedor.xlsx',index=False)
dataFrame_dcomprador.to_excel('dcomprador.xlsx',index=False)
dataFrame_dmateriaprima.to_excel('dmateriaprima.xlsx',index=False)
```


```python

```


```python
dataFramefcompras.head()
```




<div><div id=bc672053-75ad-40d5-a31a-a5f0f25c2083 style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('bc672053-75ad-40d5-a31a-a5f0f25c2083').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idRequisicao</th>
      <th>dataRequisicao</th>
      <th>dataSaida</th>
      <th>dataEntrega</th>
      <th>TemContrato</th>
      <th>quantidade</th>
      <th>custoUnitario</th>
      <th>ValorTotal</th>
      <th>idComprador</th>
      <th>idFornecedor</th>
      <th>idMateriaPrima</th>
      <th>DataPrevistaEntrega</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-120-54579-X</td>
      <td>2021-05-18</td>
      <td>2021-07-18</td>
      <td>2021-09-17</td>
      <td>Sim</td>
      <td>4</td>
      <td>926.36</td>
      <td>3705.44</td>
      <td>4314</td>
      <td>5619</td>
      <td>7203</td>
      <td>2021-07-28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0-85512-018-5</td>
      <td>2021-03-23</td>
      <td>2021-08-17</td>
      <td>2021-09-10</td>
      <td>Sim</td>
      <td>19</td>
      <td>832.18</td>
      <td>15811.42</td>
      <td>7288</td>
      <td>6688</td>
      <td>3828</td>
      <td>2021-09-05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0-85452-746-X</td>
      <td>2021-01-02</td>
      <td>2021-07-27</td>
      <td>2021-09-28</td>
      <td>Não</td>
      <td>13</td>
      <td>722.32</td>
      <td>9390.16</td>
      <td>389</td>
      <td>5904</td>
      <td>5329</td>
      <td>2021-07-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1-59815-702-7</td>
      <td>2021-03-28</td>
      <td>2021-07-25</td>
      <td>2021-09-06</td>
      <td>Sim</td>
      <td>6</td>
      <td>747.75</td>
      <td>4486.50</td>
      <td>2640</td>
      <td>1292</td>
      <td>6018</td>
      <td>2021-08-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0-264-87742-X</td>
      <td>2021-06-17</td>
      <td>2021-08-28</td>
      <td>2021-10-18</td>
      <td>Sim</td>
      <td>3</td>
      <td>568.79</td>
      <td>1706.37</td>
      <td>331</td>
      <td>2879</td>
      <td>9128</td>
      <td>2021-09-07</td>
    </tr>
  </tbody>
</table></div>




```python
dataFramfcustopadrao.head()
```




<div><div id=da40218e-6516-480b-8b8f-6869a1ff16ab style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('da40218e-6516-480b-8b8f-6869a1ff16ab').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idMateriaPrima</th>
      <th>idFornecedor</th>
      <th>custoUnitarioPadrao</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7203</td>
      <td>5619</td>
      <td>458.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3828</td>
      <td>6688</td>
      <td>108.40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5329</td>
      <td>5904</td>
      <td>433.77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6018</td>
      <td>1292</td>
      <td>434.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9128</td>
      <td>2879</td>
      <td>181.42</td>
    </tr>
  </tbody>
</table></div>




```python
dataFrame_dfornecedor.head()
```




<div><div id=c7e2cd7c-6253-42aa-926f-bf98862eb59a style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('c7e2cd7c-6253-42aa-926f-bf98862eb59a').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idFornecedor</th>
      <th>fornecedor</th>
      <th>PrazoEntregaPadrao</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5619</td>
      <td>Catarina Silveira</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6688</td>
      <td>Eduardo Moraes</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5904</td>
      <td>Yuri Cunha</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1292</td>
      <td>Nicolas Monteiro</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2879</td>
      <td>Maria Luiza Rezende</td>
      <td>10</td>
    </tr>
  </tbody>
</table></div>




```python
dataFrame_dcomprador.head()
```




<div><div id=aa51babc-bbaf-4a29-928f-a367d7768ed7 style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('aa51babc-bbaf-4a29-928f-a367d7768ed7').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idComprador</th>
      <th>comprador</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4314</td>
      <td>Ana Duarte</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7288</td>
      <td>Mariana Moraes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>389</td>
      <td>Thales Fernandes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2640</td>
      <td>Thomas da Mota</td>
    </tr>
    <tr>
      <th>4</th>
      <td>331</td>
      <td>Laís Fernandes</td>
    </tr>
  </tbody>
</table></div>




```python
dataFrame_dmateriaprima.head()
```




<div><div id=0e3f0b0b-97c6-4b39-9734-68413564c037 style="display:none; background-color:#9D6CFF; color:white; width:200px; height:30px; padding-left:5px; border-radius:4px; flex-direction:row; justify-content:space-around; align-items:center;" onmouseover="this.style.backgroundColor='#BA9BF8'" onmouseout="this.style.backgroundColor='#9D6CFF'" onclick="window.commands?.execute('create-mitosheet-from-dataframe-output');">See Full Dataframe in Mito</div> <script> if (window.commands.hasCommand('create-mitosheet-from-dataframe-output')) document.getElementById('0e3f0b0b-97c6-4b39-9734-68413564c037').style.display = 'flex' </script> <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idMateriaPrima</th>
      <th>materiaPrima</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7203</td>
      <td>LUX</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3828</td>
      <td>BOG</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5329</td>
      <td>CGQ</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6018</td>
      <td>KTM</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9128</td>
      <td>GDL</td>
    </tr>
  </tbody>
</table></div>




```python

```


```python

```


```python

```


```python

```
