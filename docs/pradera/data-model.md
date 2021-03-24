# Pradera data model


## Definitions 

* `User` a person that creates `Book`s
* `Book`  is a collection of flows, with one official (mainline? trunk? master?)
* `Block` is a content item, it can be title, paragraph, chapter. A `block` can reference other blocks 
  - Fields: `id`, `type`, `content` , `user_id`, `hash`
   
* `Flow`  is a collection of blocks ordered by the user
    `FlowItem (id, block_id, prev_block_id, comments)` 
    `Comments(flow_item_id, content, user)` 
              



## Examples  

**Official**
>Lorem Ipsum
>
>What is Lorem Ipsum?
>Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
>Lorem Ipsum has been the industry's standard dummy text ever since the 1500


**Crisoo**
>Lorem Ipsum
>
>What is Lorem?
>mi tldr
>Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
>Lorem Ipsum has been the industry's standard dummy text ever since the 1500



```yaml
blocks
  - # Block 
    id: 1
    type: TITLE
    content: Lorem Ipsum
    user: isaac
  - # Block 
    id: 2
    type: TITLE
    content: What is Lorem Ipsum?-
    user: isaac
  - # Block 
    id: 3
    type: PARAGRAPH
    content: Lorem Ipsum is simply dummy text of the printing and typesetting industry. 
    user: isaac
  - # Block 
    id: 4
    type: PARAGRAPH
    content: Lorem Ipsum has been the industry's standard dummy text ever since the 1500
    user: isaac
  - # Block 
    id: 5
    type: TITLE
    content: What is Lorem?-
    user: crisoo
  - # Block 
    id: 6
    type: PARAGRAPH
    content: mi tldr
    user: crisoo    

flows:
    official: 
        -   
            order: 1  
            block_id: 1
        - 
            order: 2 
            block_id: 2
        - 
            order: 3
            block_id: 3
        - 
            order: 4
            block_id: 4

    cris-flow: 
        - 
            order: 1
            block_id: 1
        -  
            order: 2
            block_id: 5 
            prev_block_id: 2
            comments:
                - "[cris]bla bvla bla  " 
                - "[matt]se ve muy bien, lo tomare " 
        -  
            order: 3
            block_id: 6
        -  
            order: 4
            block_id: 4    
        -  
            order: 5
            block_id: 3    


    official-with-merge: 
        -   
            order: 1  
            block_id: 1
        -  
            order: 2
            block_id: 5 
            prev_block_id: 2
            comments:
                - "[cris]bla bvla bla  " 
                - "[matt]se ve muy bien, lo tomare " 
        - 
            order: 3
            block_id: 3
        - 
            order: 4
            block_id: 4


```





## TODO 
 How do we determine the ending of a block (at capture time)