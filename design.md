



## 2. develop a suitable directed graph and search tree based on the map presented in class of Kenya’s Highway Network

**Abstraction** is where we will remove details that will do not help the agent in deciding its route. In this case this means
- **State:** a state is only the town the trailer is in. Traffic and weather is ignored
- **Actions:** Driving between two towns is treated as 1 action
- **Map:** only major towns where roads join and or split are kept, small towns are left out because the trailer cannot change route there

### The towns(Nodes)
We picked 10 towns that cover all the regions and sit at the highway junctions

| Town     | Region              | Why it was chosen                                 |
|----------|---------------------|---------------------------------------------------|
| Nairobi  | Nairobi             | Start point                                       |
| Thika    | Central Highlands   | Start of the A2 road north                        |
| Nyeri    | Central Highlands   | Main town on the Central route                    |
| Naivasha | Rift Valley         | On the main A104 road west                        |
| Narok    | Rift Valley         | Start of the southern route                       |
| Nakuru   | Rift Valley         | Junction: roads to Kericho and Eldoret split here |
| Kericho  | Rift Valley         | Junction of the Nakuru and Narok routes           |
| Eldoret  | Rift Valley         | Northern route towards Kakamega                   |
| Kakamega | Lake Victoria Basin | Last stop on the northern route                   |
| Kisumu   | Lake Victoria Basin | Goal                                              |

### The roads (Edges)

| From     | To       | Main road | Distance (km) |
|----------|----------|-----------|---------------|
| Nairobi  | Thika    | A2        | 45            |
| Nairobi  | Naivasha | A8        | 91            |
| Nairobi  | Narok    | B3        | 143           |
| Thika    | Nyeri    | A2        | 113           |
| Nyeri    | Nakuru   | B5        | 167           |
| Naivasha | Nakuru   | A8        | 70            |
| Narok    | Kericho  | B3 / C23  | 157           |
| Nakuru   | Kericho  | B1        | 107           |
| Nakuru   | Eldoret  | A8        | 156           |
| Kericho  | Kisumu   | B1        | 84            |
| Eldoret  | Kakamega | A1        | 80            |
| Kakamega | Kisumu   | A1 / A8   | 107           |

### Directed Graph
The edges point from Nairobi to Kisumu because the agent is travelling west and it stops it from going in circles.

===== DIRECTED GRAPH =====

```mermaid
graph LR
    Nairobi["Nairobi"]
    Thika["Thika"]
    Naivasha["Naivasha"]
    Narok["Narok"]
    Nyeri["Nyeri"]
    Nakuru["Nakuru"]
    Kericho["Kericho"]
    Eldoret["Eldoret"]
    Kisumu["Kisumu"]
    Kakamega["Kakamega"]
    Nairobi -->|45 km| Thika
    Nairobi -->|91 km| Naivasha
    Nairobi -->|143 km| Narok
    Thika -->|113 km| Nyeri
    Nyeri -->|167 km| Nakuru
    Naivasha -->|70 km| Nakuru
    Narok -->|157 km| Kericho
    Nakuru -->|107 km| Kericho
    Nakuru -->|156 km| Eldoret
    Kericho -->|84 km| Kisumu
    Eldoret -->|80 km| Kakamega
    Kakamega -->|107 km| Kisumu
```


### Search Tree
For the search tree, the root is Nairobi and each town is expanded into the towns it connects to. A branch stops when it reaches kisumu, each box shows the town and g the distance.

===== SEARCH TREE =====

```mermaid
graph TD
    T1["Nairobi<br/>g=0"]
    T2["Thika<br/>g=45"]
    T1 -->|45| T2
    T3["Nyeri<br/>g=158"]
    T2 -->|113| T3
    T4["Nakuru<br/>g=325"]
    T3 -->|167| T4
    T5["Kericho<br/>g=432"]
    T4 -->|107| T5
    T6["Kisumu<br/>g=516"]
    T5 -->|84| T6
    T7["Eldoret<br/>g=481"]
    T4 -->|156| T7
    T8["Kakamega<br/>g=561"]
    T7 -->|80| T8
    T9["Kisumu<br/>g=668"]
    T8 -->|107| T9
    T10["Naivasha<br/>g=91"]
    T1 -->|91| T10
    T11["Nakuru<br/>g=161"]
    T10 -->|70| T11
    T12["Kericho<br/>g=268"]
    T11 -->|107| T12
    T13["Kisumu<br/>g=352"]
    T12 -->|84| T13
    T14["Eldoret<br/>g=317"]
    T11 -->|156| T14
    T15["Kakamega<br/>g=397"]
    T14 -->|80| T15
    T16["Kisumu<br/>g=504"]
    T15 -->|107| T16
    T17["Narok<br/>g=143"]
    T1 -->|143| T17
    T18["Kericho<br/>g=300"]
    T17 -->|157| T18
    T19["Kisumu<br/>g=384"]
    T18 -->|84| T19
```