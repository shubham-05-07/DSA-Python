# Creat node for singly linked list 
class Node:
    def __init__(self, data=None, ref=None):
        self.data=data
        self.ref=ref

# Defining Singly Linked List
class SLL:
    def __init__(self,start=None):
        self.start=start
    
    def is_empty(self):
        return self.start==None
        
    def append_first(self,data):
        new_node=Node(data,self.start)
        self.start = new_node

    def append_last(self,data):
        new_node = Node(data)
        if self.start != None:
            temp=self.start
            while temp.ref != None:
                temp = temp.ref
            temp.ref = new_node
    
    def search_node(self,data):
        temp=self.start
        while temp !=None:
            if temp.data == data:
                return temp
            else:
                temp =temp.ref
        return ValueError
# """To add nord with data after particular node then we have to provide the data and also the node
# reference where to add node"""
    def append_after(self, temp, data):
        if temp != None:
            new_node = Node(data,temp.ref)
            temp.ref = new_node

    def print_list(self):
        temp = self.start
        while temp != None:
            print(temp.data,end=" ")
            temp=temp.ref
        print()
    def delete_first(self):
        if self.start != None:
            self.start = self.start.ref
    
    def delete_last(self):
        if self.start != None:
            temp =self.start
            while temp.ref.ref != None:
                temp = temp.ref
            temp.ref = None
    
    def delete_node_value(self,value):
        if self.start == None:
            pass
        elif self.start.ref == None:
            if self.start.data ==value:
                self.start = None
        else:
            temp= self.start
            if temp.data == value:
                self.start = temp.ref
            else:
                while temp.ref != None:
                    if temp.ref.data == value:
                        temp.ref = temp.ref.ref
                        break
                    temp=temp.ref

    def reverse_list(self):
        pre = None
        current = self.start
        while current != None:
            next_node = current.ref
            current.ref = pre
            pre = current
            current = next_node
        self.start = pre

    def get_nth(self,n):
        count= 1
        temp = self.start
        while temp!= None:
            if count == n:
                print(temp.data)
            count+=1
            temp = temp.ref
         

    def __iter__(self):
        return SLLIterator(self.start)

class SLLIterator:
    def __init__(self,start):
        self.first = start
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.first == None:
            raise StopIteration
        data=self.first.data
        self.first = self.first.ref
        return data
