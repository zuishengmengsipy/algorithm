# Initial page

## 二叉树遍历算法

### 1. 先序遍历 <a id="_1-&#x5148;&#x5E8F;&#x904D;&#x5386;"></a>

* 递归

  ```text
  void scan(BiTree T) {
      if(T!=NULL){
          cout<<T->data;
          scan(b->lchild);
          scan(b->rchild);
      }
  }
  ```

* 非递归

  ```text
    //先序遍历非递归
    void InOrder(BiTree T){
        BiTree p = T;
        InitStack S;
        while(p || !is_empty(S)){
            if(p){
                cout<<p->data;
                push(S,p);
                p=p->lchild;
            }
            else{
                pop(S,p);
                p = p->rchild
            }
        }
    }
  ```

### 2. 中序遍历 <a id="_2-&#x4E2D;&#x5E8F;&#x904D;&#x5386;"></a>

* 递归

  ```text
  void scan(BiTree T) {
    if(T != null) {
        scan(T->lchild);
        cout<<T->data;
        scan(T->rchild);
    }
  }
  ```

* 非递归

  ```text
    //中序遍历非递归
    void InOrder(BiTree T){
        BiTree p = T;
        InitStack S;
        while(p || !is_empty(S)){
            if(p){
                push(S,p);
                p=p->lchild;
            }
            else{
                pop(S,p);
                cout<<p->data;
                p = p->rchild
            }
        }
    }
  ```

### 3. 后序遍历 <a id="_3-&#x540E;&#x5E8F;&#x904D;&#x5386;"></a>

* 递归

  ```text
  void scan(BiTree T) {
    if(T != null) {
        scan(T->lchild);
        scan(T->rchild);
        cout<<T->data;
    }
  }
  ```

* 非递归

  ```text
    //后序遍历非递归
    void PostOrder(BiTree T){
        InitStack(S);
        p = T;
        r = NULL; //最近访问过的结点
        while(p || !is_empty(S)){
            if(p){
                Push(S,p); //二叉树左子树均入栈，先找到最左结点
                p = p->lchild;
            }
            else{
                GetTop(S,p);//获得栈顶元素，并不弹栈
                if(p->rchild && r!=p->rchild){//右孩子存在且未被访问过
                    p = p->rchild;
                    Push(S,p);//右孩子进栈
                    p = p->lchild; //再走到右孩子的最左
                }
                else{ //若既无左孩子也无右孩子，则弹出结点并访问
                    Pop(S,p); 
                    cout<<P->data;
                    r = p; //置为最近访问结点
                    p = NULL; //p重置
                    //因为弹栈相当于一个结点（包括左右孩子）已经被访问完，
                    //所以要置空走else继续遍历
                }
            }
        }
    }
  ```

### 4. 层次遍历 <a id="_4-&#x5C42;&#x6B21;&#x904D;&#x5386;"></a>

```text
void LevelOrder(BiTree T){
    BiTNode p;
    SqQueue Q;
    InitQueue(Q):
    EnQueue(Q,T);
    while(!isEmpty(Q)){ //队列非空
        DeQueue(Q.p);//结点出队，并获取该结点给p
        visit(p); //cout<<p->data;
        //结点左右孩子入队
        if(p->lchild!=NULL)
            EnQueue(Q,p->lchild);
        if(p->rchild!=NULL)
            EnQueue(Q,p->rchild);
    }
}
```

若已知以下三种序列组合，则可以唯一的确定一颗二叉树

* 先序和中序序列（前序为进栈序列，中序为出栈序列）
* 后序和中序序列
* 层次和中序序列

> * 若非空二叉树先序序列和后序序列正好相反，则二叉树形态是什么?
>
>   每层只有一个结点，高度=结点个数
>
> * 若非空二叉树先序序列和后序序列正好相同，则二叉树形态是什么？
>
>   只有根节点

## 二叉树的统计算法

### 1. 统计二叉树中度为2的结点个数 <a id="_1-&#x7EDF;&#x8BA1;&#x4E8C;&#x53C9;&#x6811;&#x4E2D;&#x5EA6;&#x4E3A;2&#x7684;&#x7ED3;&#x70B9;&#x4E2A;&#x6570;"></a>

```text
int Dnode(BiTree T){
    if(T==NULL) 
        return 0;
    else if(T->lchild && T->rchild)
        return Dnode(T->lchild)+Dnode(T->rchild) + 1;
    else
        return Dnode(T->lchild)+Dnode(T->rchild);    
}
```

### 2. 统计二叉树中度为1的结点个数 <a id="_2-&#x7EDF;&#x8BA1;&#x4E8C;&#x53C9;&#x6811;&#x4E2D;&#x5EA6;&#x4E3A;1&#x7684;&#x7ED3;&#x70B9;&#x4E2A;&#x6570;"></a>

```text
int Lnode(BiTree T){
    if(T==NULL)
        return 0;
    else if(T->lchild==NULL&&T->rchild!=NULL || T->lchild!=NULL&&T->rchild==NULL)
        return Lnode(T->rchild)+Lnode(T->lchild)+1;
    else
        return Lnode(T->rchild) + Lnode(T->lchild);
}
```

### 3. 统计二叉树中度为0的结点个数\(叶子\) <a id="_3-&#x7EDF;&#x8BA1;&#x4E8C;&#x53C9;&#x6811;&#x4E2D;&#x5EA6;&#x4E3A;0&#x7684;&#x7ED3;&#x70B9;&#x4E2A;&#x6570;&#x53F6;&#x5B50;"></a>

```text
int Leaves(BiTree T){
    if(T==NULL)
        return 0;
    else if(T->lchild==NULL && T->rchild==NULL)
        return 1;
    else 
        return Leaves(T->rchild) + Leaves(T->lchild);
}
```

### 4. 统计二叉树的高度 <a id="_4-&#x7EDF;&#x8BA1;&#x4E8C;&#x53C9;&#x6811;&#x7684;&#x9AD8;&#x5EA6;"></a>

```text
int Height(BiTree T){
    if(T==NULL)
        return 0;
    else if(!T->lchild && !T->rchild)
        return 1;
    else{
        int hl = Height(T->lchild);
        int hr = Height(T->rchild);
        return (hl>hr?hl:hr) + 1;
    }
}
```

### 5. 统计二叉树的宽度 <a id="_5-&#x7EDF;&#x8BA1;&#x4E8C;&#x53C9;&#x6811;&#x7684;&#x5BBD;&#x5EA6;"></a>

```text
//开辟一个数组count[二叉树高度],遍历每一个节点,然后根据当前节点所在层次i,则执行count[i]++;
//先序遍历，一层遍历完成后进行宽度比较
int count[100];
int Width(BiTree T,int i){ //i表示层数，初始为1
    int max = -1;  //最大宽度
    if(T==NULL)
        return 0;
    count[i] ++; //第i层宽度++
    if(max<count[i])  //比较。最终决定性的比较在右子树遍历完成的比较
        max = count[i];
    else{
        Width(T->lchild,i+1);
        Width(T->rchild,i+1);
    }
}
```

## 二叉树基本操作算法

### 1.反向层次遍历（自下而上，从右到左） <a id="_6-&#x8BA1;&#x7B97;&#x6307;&#x5B9A;&#x7ED3;&#x70B9;p&#x6240;&#x5728;&#x5C42;&#x6B21;"></a>

在原来的层次遍历算法的基础上加上栈的基本操作。在出队的同时将各节点入栈，在所有的节点全部入栈后，依次出栈访问便可解决该问题。

```text
void InLevelOrder(BiTNode T){
    BiTNode p;
    if(T==Null){
        return;
    }
    SqQueue Q;
    InitQueue(Q); //队列初始化
    SqStack S;    
    InitStack(S); //栈初始化
    EnQueue(Q,T);  
    while(!IsEmpty(Q)){ //当队列非空，正常顺序层次遍历
        DeQueue(Q,P);   //当前结点出队
        Push(S,p);      //出队的当前结点入栈
        //左右孩子入队
        if(p->lchild){
            EnQueue(Q,p->lchild);
        }
        if(p->rchild){
            EnQueue(Q,p->rchild);
        }
    }
    //将所有节点出栈访问
    while(!IsEmptyStack(S)){  //栈不空，则遍历栈
        Pop(S.p);
        cout<<p->data;
    }
}
```

### 2. 计算指定结点\*p所在层次 <a id="_6-&#x8BA1;&#x7B97;&#x6307;&#x5B9A;&#x7ED3;&#x70B9;p&#x6240;&#x5728;&#x5C42;&#x6B21;"></a>

```text
int Level(BiTree T, BiTNode *p, int level){
    if(T==NULL)
        return 0;
    else if(T->data == p->data)
        return level;
    else{
        int l = Level(T->lchild,p,level+1);
        if(l!=0)
            return l;
        else
            return Level(T->rchild,p,level+1);
    }
}
```

### 3. 交换二叉树中每个结点的两个子女 <a id="_7-&#x4EA4;&#x6362;&#x4E8C;&#x53C9;&#x6811;&#x4E2D;&#x6BCF;&#x4E2A;&#x7ED3;&#x70B9;&#x7684;&#x4E24;&#x4E2A;&#x5B50;&#x5973;"></a>

```text
//先交换左右孩子的左右子树，再交换左右孩子
void swap(BiTree T){
    if(T){
        swap(T->lchild);
        swap(T->rchild);
        int temp = T->lchild;
        T->lchild = T->rchild;
        T->rchild = temp;
    }
}
```

### 4.查找二叉树祖先

后序遍历非递归算法。当访问到值为k的节点时，栈中所有元素都是祖先，依次出栈

```text
void Ancestor(btree t,elemtype k){
    initstack(s);        //初始化栈
    btnode *p=t,r=null;  //r记录最新访问节点
    while(p||!empty(s)){ //p不为空，且栈不为空
        if(p){           //走到最左边（未必是叶节点）
            push(s,p);   //进栈
            p=p->lchild; //无左节点时不再进入，栈顶为最左结点
        }
        else{
            gettop(s,p); //获取栈顶元素判断是否为叶节点，或者是否为从右子树返回
            if(p->rchild&&p->rchild!=r){   //右子树存在且不是从右子树返回
                push(s,p->rchild);
                p=p->rchild->lchild;       //转到右子树的左孩子
            }
            else{                          //p为叶节点，或者从右子树返回根节点
                pop(s,p);
     -------------
                if(p->data==k){            //找到k节点，输出栈内元素，并退出
                    outputstack(s);
                    return ;
                }//除了这部分if（），其余都是后序遍历非递归算法
     -------------
                r=p; //记录最新访问（出栈）的节点
                p=null; //p置为空，以防再次入栈
             }//else
         }//else
     }//while
}
```

### 5.构造中序线索二叉树

```text
void CreateInThread(ThreadTree T){
    Threadtree pre = NULL；
    if(T!=NULL){
        Thread(T,pre);
        pre->rchild=NULL;
        pre->rtag=1;
    }
}

void InThread(ThreadTree &p, ThreadTree &pre){
    if (p != null)
    {
        InThread(p->lchild, pre);    
        //对左孩子递归，自然第一个操作的结点为最左下结点（不一定为叶结点）
        if (p->lchild == NULL) //如果左子树为空，建立前驱线索
        {
            p->lchild = pre; //将前一个结点地址为前驱线索
            p->ltag = 1;     //标志左子树域已经设置为前驱线索
        }
        if (pre != NULL && pre->rchild == NULL)
        {//若前驱结点不是空，且前驱结点的右子树为空时
            pre->rchild = p;  //设置前驱结点的后继为当前结点
            pre->rtag = 1;    //标志前驱结点的右子树域已经设置为后继线索
        }
        pre = p; 
        //当p将要离开一个访问过的结点时，pre指向p，所以p指向新结点时。pre是p的前驱
        p = p->rchild; //p指向右孩子，准备将右子树线索化
        InThread(p, pre);
    }
}
```

### 6.遍历中序线索二叉树

```text
ThreadNode *First(ThreadNode *p){//寻找中序线索二叉树的第一个结点（最左结点）
    while(p->ltag == 0)
        p=p->lchild;
    return p; //寻找树的最左下角结点，不一定是叶节点
}

ThreadNode *Next(ThreadNode *p){//返回后继结点
    if (p->tag == 0)
        return First(p->rchild); 
        //中序遍历下，p结点的后继结点是p的右子树中最左结点，通过First()返回即可
    else
        return p->rchild; //rtag==1，此时rchild为线索，指向结点的直接后继
}

void InOrder(ThreadNode *root){//遍历
    for (ThreadNode *p = First(root) ; p !=NULL ; p = Next(p))
    {
        //对结点操作
    }
}
```



```text
// 在root为根的二叉树中找A,B的LCA:
// 如果找到了就返回这个LCA
// 如果只碰到A，就返回A
// 如果只碰到B，就返回B
// 如果都没有，就返回null
TreeNode LCARec(TreeNode root, TreeNode rootA, TreeNode rootB) {

 if(root == null || root == rootA || root == rootB) {
     return root;
 }

 TreeNode left = LCARec(root.left, rootA, rootB);
 TreeNode right = LCARec(root.right, rootA,rootB);

 if(left != null && right != null) {
     return root;
 }

 if(left != null) {
     return left;
 }

 if(right != null) {
     return right;
 }

 return null;

}

```

