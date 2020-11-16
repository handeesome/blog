---
title: "Flutter Notes"
date: 2020-06-21T13:19:04+02:00
draft: false

categories: []
tags: []
author: ""
---

# flutter Syntax

This article is written before I actually started doing anything relate to Flutter project, and during my first flutter project I did not record what I did, what I have is the final code about two identity page I wrote for the school startup PRYZL. [*go to the project here*](/)

```
void main() => runApp(MaterialApp(
    home: (), 
    initialRoute(): `'/home'`,
    routes:{
        `'/': (context) => Loading()`,
    }
));
```

* StatelessWidget:
    * Inside this you will have to declare some instances.
```
StatefulWidget:
    - setState((){})
    - Future.delayed(Duration(seconds: 3)) 
```
    (async and await if want to make a delayed function call first)

* use for `await`:
    ```
    String one = await Future.delayed(Duration(seconds: 1){ return 1})
    ```

```
Basic Widges:
    - Scaffold
        - appBar: AppBar
            - title: Text('')
            - centertitle: true
            - backgroundColor: Colors.red[10]
            - elevation: 0.0
        - body: 
            - Center
                - child:
                    - Text
                        - style: Textstyle( fontsize: 20, )
                    - Icon
                        - Icon.airport_shuttle
                    - IconButton
                        - 
                    - RaisedButton
                        - onPressed: () { print('')}
                        - icon: Icon()
                        - label: Text()
                        - color: Colors. 
                    - FlatButton
                        - child: Test('')
                    - Image.asset('assets/img.jpg')
                    - Image.network('URL')
            - Container
                - padding (inside the container)
                    - EdgeInsets.all
                - margin (around the container)
                    - EdgeInsets
                - color
                - child 
            - Padding
                - no color
                - no margin
                - padding
                - child
            - Row
                - mainAxisAlignment: MainAxisAlignment.center
                - crossAxisAlignment: CrossAxisAlignment.stretch
                - children: <Widget> [] //list of Widgets
                    - Text
                    - FlatButton
                    - Container
                    - Expanded
                - SizedBox(height:10.0)
            - Column
                - CircleAvatar
                    - backgroundImage
                    - radius
                - children
                    - toList
                - Row (row in column)
                - SizedBox(`width:10.0`)
                - Divider
                    - height
                    - color
        - floatingActionButton
            - onPressed
                - setState( () {} )
            - child: Icon(Icons.)
            - backgroundColor
```


reference : https://www.youtube.com/watch?v=jAxNZYX7mHM&list=PL4cUxeGkcC9jLYyp2Aoh6hcWuxFDX6PBJ&index=20
