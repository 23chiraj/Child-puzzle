<h1> Most Annoying childhood puzzle </h1>
<h2>Puzzle which annoys me and You the most in our Childhood. Solved by basic Artificial Intelligence!!!!!!!!!</h2>
<img src='https://raw.githubusercontent.com/mohitrajain/Most-Annoying-Puzzle-childhood/master/images.jpg' ></img>
<h1>node solution.js </h1>

```
var i = 0;
var j = 0;
// var success to check for success(1) or failure(0)
var success = 0;

// A shows different available paths for each (index + 1) node to move
var A = [[2,3],[1,3,4,6,7],[1,2,5,6,7],[2,6],[3,7],[2,3,4,7,8],[2,3,5,6,8],[6,7]];

// B will take care of nodes through which dfs has traced in current run
var B =[[],[],[],[],[],[],[],[],[]];

// S shows current dfs path
var S = [];

// constructor function constructs node for us with (parent,children,value) info
function node(val,par,node) {
    var self = this;
    this.parentnode = par;
    this.nodeno = node;
    this.val = val;
    this.children =[];
    (function(self){
        var x =self.val - 1;
       for(var i in A[x]){
           if(B[x].indexOf(A[x][i]) <0)
             self.children.push(A[x][i]);
       }
    }(self));
}

// global object to which nodes created while whole execution will be attached
var obj = {};

// initial object through which dfs will proceed
obj[i++] = {
    parentnode:-1,
    nodeno:0,
    val:9,       // here 9 is taken as arbitrary value just for initialization
    children:[1,2,3,4,5,6,7,8]
};

//S.push(2);
//S.push(3);
//join(1,3);
//obj[i] = new node(2,-1,i++);

function join (x,y){
    B[x-1].push(y);
    B[y-1].push(x);
}

function unjoin(x,y) {
    j++;
    B[x-1].pop(y);
    B[y-1].pop(x);
}

var cur = obj[0];
var y;

// this while loop will take care of backtracking and proceeding of dfs
// exiting condition for while loop are chosen such that if all of the children of initial object are tried than exit
// or if we find our goal state i.e. 14 line segments or 15 points in our any dfs path
while(obj[0].children.length > -1){

    if(cur.children.length === 0) {
        if(cur.nodeno === 0)
            break;
        S.pop(cur.val);
        unjoin(cur.val,obj[cur.parentnode].val);
        cur = obj[cur.parentnode];
        //console.log(cur.children);
    }

    else{
    y =cur.children[cur.children.length - 1];
    cur.children.pop(y);
     S.push(y);
        if(S.length === 15)
        {
            success = 1;
            break;
        }
        console.log(S);
        join(cur.val,y);
    obj[i] = new node(y,cur.nodeno,i++);
    cur = obj[i-1];
    }

        }

if(success)
    console.log('Solution is : ' + S);
else
    console.log('No Solution is found ! Thank God');

//console.log(B);

// i will show number of nodes created
console.log(i);

// i will count number of different paths or dfs choose before winning or losing
console.log(j);
```
