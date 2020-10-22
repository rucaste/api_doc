## Local

Este é um objecto que representa um local físico que agrupa um conjunto de contentores.
É possível obter um conjunto de locais ou a informação de cada local isoladamente. 

ENDPOINT:

```http request
api/contentores/locais
```

&nbsp
### O objecto local

Cada objecto poder ser obtido isoladamente através do seu id utilizando o endpoint, por exemplo:
 
```http request 
api/contentores/locais/2517
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

#### Atributos

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


#### Opções de filtragem

Os filtros deveram ser adicionados após o simbolo `?` Separando cada filtro por `&` por exemplo

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



.

.

.

.

.


datainicio, datafim, data_ultima_recolha, data_ultima_lavagem

qualquer destes critérios de filtragem tem de ser utilizado da seguinte forma,

se $criterio for o nome do critério a utilizar (datainicio, datafim, data_ultima_recolha, data_ultima_lavagem), temos as seguintes opções






