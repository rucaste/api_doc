# Local

Este é um objecto que representa um local físico que agrupa um conjunto de contentores utilizados para a deposição de resíduos.
É possível obter um conjunto de locais ou a informação de cada local isoladamente. 

ENDPOINT:

```http request
api/contentores/locais
```

&nbsp;
## O objecto local

Cada objecto poder ser obtido isoladamente através do seu id utilizando o endpoint, por exemplo:
 
```http request 
GET api/contentores/locais/2517
```

devolve o objecto com id igual a 2517, com a seguinte estrutura:

```json 
{
    "id": 2517,
    "tipo": "Indiferenciado",
    "circuitos": [
        "ind_180",
        "ind_120"
        ],
    "codigolocal": "002633",
    "local": "N247",
    "localidade": "Alcabideche",
    "rua": "Rua do Cabo",
    "numero": "0",
    "ativo": true,
    "geom": {
        "type": "Point",
            "coordinates": [
                -9.471229553,
                38.764690399
            ]
        },
    "datainicio": "2018-05-06",
    "datafim": null,
    "elementos": [
        "Cais",
        "Fixador",
        "IND800"
        ],
    "data_ultima_recolha": null,
    "data_ultima_lavagem": "2020-08-25",
    "niveis_dict": {
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0,
        "5": 0,
        "Sem nível": 0
        },
    "contentores": [
        {
            "id": 4173,
            "idcontentor": "481824",
            "idtransponder": "962C391000004000",
            "produto": "ind",
            "tipo": "IND800",
            "capacidade": 800,
            "datainicio": "2018-05-06",
            "datafim": null,
            "circuitos": [
                "ind_180",
                "ind_120"
                ],
            "ativo": true,
            "data_ultima_recolha": null,
            "data_ultima_lavagem": "2020-08-25",
            "niveis_dict": {
                "1": 0,
                "2": 0,
                "3": 0,
                "4": 0,
                "5": 0,
                "Sem nível": 0
                }
            }
        ]
    }
```

&nbsp;
### Atributos

Atributo | Tipo | Descrição | Opções
-------- | ---- | --------- | ------
id | inteiro | chave primaria do objecto | 
tipo | string | categoria do local | <li>Domicílios</li><li>Stock</li><li>Comercial</li><li>Industrial</li><li>Aterro</li><li>Grande produtor</li><li>Seletiva</li><li>Misto</li><li>Indiferenciado</li><li>Usuário doméstico</li>  
circuitos | string | nome dos circuitos que estão associados a um ou mais contentores que fazem parte do local |
codigolocal | string | código único de identificação do local no sistema MOBA |
local | string | parte da morada conforme definido no sistema MOBA |
localidade | string | parte da morada conforme definido no sistema MOBA |
rua | string | parte da morada conforme definido no sistema MOBA |
numero | string | parte da morada conforme definido no sistema MOBA |
ativo | boleano | estado | <li>True</li><li>False</li> 
geom | objecto geoespacial (ponto) | localização geoespacial do local (srid=4326) |
datainicio | data | data de inserção do local no sistema MOBA |
datafim | data | data de desativação do local |
data_ultima_recolha | data | data da recolha mais recente de qualquer contentor que pertence ao local |
data_ultima_lavagem | data | data da lavagem mais recente de qualquer contentor que pertence ao local |
elementos | array de strings | chave primaria do objecto |
id | string | lista com a identificação do tipo de contentor, ou cais, ou fixador que constituem o local |
niveis_dict | objecto | contagem dos níveis de enchimento do total de recolhas dos contentores do local. Apenas aplicável a contentores de papel, plástico e vidro |
contentores | array de objectos | lista com objectos do tipo contentor |    


&nbsp;
## Listas de Locais

As listagens de locais podem ser obtidas no endpoint respectivo, é possível filtar e ordenar os resultados.

```http request
api/contentores/locais/
```
A resposta venda seguinte forma:

```json
{
    "count": 374,
    "next": "https://cabi.pt/apiv2/contentores/locais2/?page=7&tipo=sele",
    "previous": "https://cabi.pt/apiv2/contentores/locais2/?page=9&tipo=sele",
    "results": [ 
       "local1",
       "local2",
       "..."
       "localn"
       ],
}
```
Por prédefinição as respostas vêm paginadas com 20 objectos, sendo possível alterar o número de registos de cada página através do query parameter ‘per_page’ até ao máximo de 100000 registos. Deste modo:

```http request
api/contentores/locais
```
devolve os resultado com 20 elementos por página
```http request
api/contentores/locais/?per_page=1000
```

devolve os resultado com 1000 elementos por página

Onde:
* `count` representa o total de objectos devolvidos
* `next` representa o link para a pŕoxima página
* `previous` representa o link para a página anterior
* `results` é a lista de resultados até ao máximo do número de elementos por página


&nbsp;
### Opções de filtragem

è possível Os filtros deveram ser adicionados após o simbolo `?` Separando cada filtro por `&` por exemplo

```http request
api/contentores/locais/?tipo=indiferenciado&local=alcabideche
```

##### tipo

Filtrar por `tipo` devolve todos os resultados que contém o parâmetro de pesquisa no atríbuto tipo.
A pesquisa não é case sensitive, exemplo:

```http request
api/contentores/locais/?tipo=indifer
```


##### circuito

Filtrar por `circuito` devolve todos os resultados que contém o parâmetro de pesquisa em qualquer elemento do array circuitos.
A pesquisa não é case sensitive, exemplo:


```http request
api/contentores/locais/?circuitos=nd_11
```

##### codigolocal

Filtrar por `codigolocal` devolve todos os resultados com codigolocal igual ao parâmetro.

Filtrar por `codigolocal__iexact` devolve todos os resultados com codigolocal igual ao parâmetro, de modo não case sensitive.

Filtrar por `codigolocal__icontains` devolve todos os resultados que o codigolocal contém o parâmetro, de modo não case sensitive.

```http request
api/contentores/locais/?codigolocal__icontains=002
```


##### local

Filtrar por `local` devolve todos os resultados com local igual ao parâmetro.

Filtrar por `local__iexact` devolve todos os resultados com local igual ao parâmetro, de modo não case sensitive.

Filtrar por `local__icontains` devolve todos os resultados que o local contém o parâmetro, de modo não case sensitive.

```http request
api/contentores/locais/?local__iexact=002
```


##### localidade

Filtrar por `localidade` devolve todos os resultados com localidade igual ao parâmetro.

Filtrar por `localidade__iexact` devolve todos os resultados com localidade igual ao parâmetro, de modo não case sensitive.

Filtrar por `localidade__icontains` devolve todos os resultados que o localidade contém o parâmetro, de modo não case sensitive.

```http request
api/contentores/locais/?localidade=002
```

##### rua

Filtrar por `rua` devolve todos os resultados com rua igual ao parâmetro.

Filtrar por `rua__iexact` devolve todos os resultados com rua igual ao parâmetro, de modo não case sensitive.

Filtrar por `rua__icontains` devolve todos os resultados que o rua contém o parâmetro, de modo não case sensitive.

```http request
api/contentores/locais/?rua__icontains=abril
```

##### numero

Filtrar por `numero` devolve todos os resultados com numero igual ao parâmetro.

Filtrar por `numero__iexact` devolve todos os resultados com numero igual ao parâmetro, de modo não case sensitive.

Filtrar por `numero__icontains` devolve todos os resultados que o numero contém o parâmetro, de modo não case sensitive.

```http request
api/contentores/locais/?numero=7054
```

##### elementos

Filtrar por `elementos` devolve todos os resultados que contém o parâmetro de pesquisa em qualquer elemento do array elementos.
A pesquisa não é case sensitive, exemplo:


```http request
api/contentores/locais/?elementos=cais
```

##### esta_ativo

Filtrar por `esta_ativo` devolve todos os resultados em que o ativo é igual ao parâmetro


```http request
api/contentores/locais/?esta_ativo=True
```

##### contentores

Filtrar por `contentores_count` devolve todos os resultados em que o número de contentores é igual ao parãmtreo de pesquisa.

Filtrar por `contentores_count__lte` devolve todos os resultados em que o número de contentores é menor ou igual ao parãmtreo de pesquisa. de modo não case sensitive.

Filtrar por `contentores_count__gte` devolve todos os resultados em que o número de contentores é maior ou igual ao parãmtreo de pesquisa.

```http request
api/contentores/locais/?contentores_count__gte=50
```

#### datas

A filtragem por os atríbutos de data (datainicio, datafim, data_ultima_recolha, data_ultima_lavagem) funcionam todas do mesmo modo

Se $atr for o nome do atríbuto a utilizar, temos as seguintes opções


query | Tipo de parâmetro  | devolve todos os registo com:
-------- | ---- | ---------
$atr__lte | data (`d`) | a data do critério menor ou igual q `d` | 
$atr__lt | data (`d`)  | a data do critério menor que `d` | 
$atr__gte | data (`d`)  | a data do critério maior ou igual a `d` |
$atr__gt | data (`d`)  | a data do critério maior que `d` |
$atr__dias | inteiro (`n`) | a data do critério ocorreu nos últimos `n` dias |

Exemplos:


```http request
api/contentores/locais/?datainicio__dias=50

api/contentores/locais/?data_ultima_recolha__gte=2020-01-01
```

&nbsp;
### Opções de ordenação

Os resultados podem ser ordenados utilizando os seguintes atributos:
```http request
codigolocal
local
localidade
rua
numero
esta_ativo
datainicio
datafim
data_ultima_recolha
data_ultima_lavagem
tipo
```

Para se ordenar utilizar-se o parametro `ordering` que pode conter um número indiscriminado de argumentos.

O nome do atriuto ordena por esse campo por ordem crescente, caso se precedido de `-`, a ordem é descrescente.

Por exemplo:


```http request
api/contentores/locais/?ordering=datafim,-rua,-local
```
Ordena os resultados primeiro através da `datafim` por ordem crecente, depois através da `rua` por ordem decrescente e finalmente através de `local` tabḿe por ordem decrescente


&nbsp;
&nbsp;
# Contentor

