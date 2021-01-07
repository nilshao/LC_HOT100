# 模版：

## 不区分layer




## 区分layer

需要layer和nextlayer

```C++

class Solution {
public:
    Node* connect(Node* root) {
        if(root == nullptr){ 
            return root;
        }
        queue<Node*> layer;
        queue<Node*> nextlayer;
        layer.push(root);
        
        while(!layer.empty()){
            Node* currentNode =layer.front();
            if(currentNode->left){ nextlayer.push(currentNode->left); }
            if(currentNode->right){nextlayer.push(currentNode->right);}
            layer.pop();
            if(layer.empty()){
                //当本层最后结点时的操作operation;
                operation();
                layer = nextlayer;
                nextlayer={};
            }
            else{
                //非最后结点时的操作operation
                operation();
            }
        }
        return root;
    }
};

```

