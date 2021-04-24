<img src="Logo.png">

<br>
<br>
<br>
<br>

<img src="ir.png">

<br><br><br><br><br><br>

<blockquote style="margin-left:290px;">
<p><em>writer:</em></p>
<blockquote>
<h2> <strong>Aniran Mohammadpour</strong></h2>
</blockquote>
</blockquote>
<blockquote style="margin-left:290px;">
<p><em>Adviser:</em></p>
<blockquote>
<h3> Dr. Fatemeh Daneshfar</h3>
</blockquote>
</blockquote>

<blockquote style="margin-left:290px;">
<p><em>Data:</em></p>
<blockquote>
<h3 > 4/24/2021</h3>
</blockquote>
</blockquote>




<br><br><br><br><br><br><br><br><br>

<img src="ir.jpg">

# Positional Index Algorithm

### Input

<img src = "2.11.jpg">


```python
docFreq_1 = { "word" : "to" , "frequency" : 993427,
                              "data" : 
                             [ { "doc_id" :  1 ,
                                  "count" :  6 ,
                                  "pos"   : [ 7, 18, 33, 72, 86, 231]
                                },
                                { "doc_id" :  2 ,
                                  "count" :  5 ,
                                  "pos"   : [ 1, 17, 74, 222, 255]
                                },
                                { "doc_id" :  4 ,
                                  "count" :  5 ,
                                  "pos"   : [ 8, 16 , 190, 429, 433]
                                },
                                { "doc_id" :  5 ,
                                  "count" :  2 ,
                                  "pos"   : [ 363, 367 ]
                                },
                                { "doc_id" :  7 ,
                                  "count" :  3 ,
                                  "pos"   : [ 13, 23, 191]
                                }
                             ]
                            }

docFreq_2 = { "word" : "be" , "frequency" : 178239,
                              "data" : 
                             [ { "doc_id" :  1 ,
                                  "count" :  2,
                                  "pos"   : [ 17, 25]
                                },
                                { "doc_id" :  4 ,
                                  "count" :  5 ,
                                  "pos"   : [ 17, 191, 291, 430, 434]
                                },
                                { "doc_id" :  5 ,
                                  "count" :  3 ,
                                  "pos"   : [  14, 19, 101 ]
                                }
                             ]
                            }
```

### Algorithm

<img src="2.12.jpg" >


```python

def positionalIntersect(doc_1, doc_2, k =1):
    
    answer = []                
    data_1 = doc_1["data"]
    data_2 = doc_2["data"]
    
    i = 0
    j = 0

    while ( i < len(data_1) and j < len(data_2)):
        doc_id_1 = data_1[i]["doc_id"]
        doc_id_2 = data_2[j]["doc_id"]
        if ( doc_id_1 == doc_id_2):
            pos_res = [] 
            pos_1 = data_1[i]["pos"]
            pos_2 = data_2[j]["pos"]

            k = 0
            
            while ( k < len(pos_1) ):
                l = 0
                while (l < len(pos_2)) :
                    distance =  abs(pos_1[k] - pos_2[l])
                    if ( distance <= k):
                        pos_res.append(l)
                    elif pos_2[l]  > pos_1[k]:
                        break
                    l = l + 1

                for item in pos_res:
                    distance =  abs(pos_2[item] - pos_1[k] )
                    if distance > k :
                        pos_res.remove(item)
                for item in pos_res:
                    answer.append({ "doc_id" : doc_id_1,  "pos_data_1" : pos_1[k]  ,  "pos_data_2" : pos_2[item] }  )
                
                k = k + 1

            i = i + 1
            j = j + 1
        else:
            if doc_id_1 < doc_id_2:
                i = i + 1
            else:
                j = j + 1

    return answer


results = positionalIntersect(docFreq_1, docFreq_2, 4)
print("Answers : ")
for res in results:
    print("Document id :" , res["doc_id"] ,  " Position Data 1: " , res["pos_data_1" ], " Position Data 2 :", res["pos_data_2" ])
```

    Answers : 
    Document id : 1  Position Data 1:  18  Position Data 2 : 17
    Document id : 4  Position Data 1:  16  Position Data 2 : 17
    Document id : 4  Position Data 1:  190  Position Data 2 : 191
    Document id : 4  Position Data 1:  429  Position Data 2 : 430
    Document id : 4  Position Data 1:  433  Position Data 2 : 430
    Document id : 4  Position Data 1:  433  Position Data 2 : 430
    Document id : 4  Position Data 1:  433  Position Data 2 : 434
    

<br><br><br><br>

University of Kurdistan information retreival course homework 

Aniran Mohammadpour

UID: 9617023136

Date: 4/24/2021
