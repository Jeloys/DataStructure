# 关于数组和链表的几个必知必会的代码实现

## 数组

### 实现一个支持动态扩容的数组

```java
package Day1;

/*
 * 实现一个支持动态扩容的数组
 */

public class DynamicArray {
	static int[] array = new int [2];//初始数组
	
	
	public static int[] addLengthArray(int[] array) {
		int[] newArray = new int[array.length*2];//自动扩容两倍
		System.arraycopy(array, 0, newArray, 0, array.length);
		//此处使用System.arraycopy(Object src,int srcPos,Object dest,int destPos, int length) ;
		return newArray;
	}
	
	
	public static void main(String[] args) {
		for (int i = 0; i < array.length; i++) {
			array[i] = i;
		}
		array = addLengthArray(array);
		for (int i = 0; i < array.length; i++) {
			System.out.println(array[i]);
		}
		
	}
}
```
输出为：  
```
0
1
0
0
```

### 实现一个大小固定的有序数组，支持动态增删改操作

## 实现两个有序数组合并为一个有序数组
```java
public class MergeTwoSortArrays {
	
	public void merge(int[] nums1, int m, int[] nums2, int n) {
		int i = m - 1, j = n - 1, k = m + n - 1;
		while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) nums1[k--] = nums1[i--];
            else nums1[k--] = nums2[j--];
        }
        while (j >= 0) nums1[k--] = nums2[j--];
    }
}
```

## 链表

### 实现单链表、循环链表、双向链表、支持增删操作

**单链表**
```java
package Day1;

/*
 * 单链表的增删操作
 */
public class MyLinkedList {
	Node head = null;	//链表头结点
	class Node{
		int val;
		Node next;
		public Node(int val) {
			this.val = val;
			next = null;
		}
	}
	
	/*
	 * 项链表中插入数据data
	 */
	public void addNode(int data) {
		Node newNode=new Node(data);
		if (head == null) {
			head = newNode;
		}else {
			search().next = newNode;
		}
	}
	
	//获得链表尾部结点
	public Node search() {
		Node lastnode = head;
		while(lastnode.next != null) {
			lastnode = lastnode.next;
		}
		return lastnode;
	}
	
	//查找链表中某个数据为value的结点并返回
	public Node search(int value) {
		Node lastnode = head;
		while(lastnode.next != null) {
			if(lastnode.val == value) {
				return lastnode;
			}
			lastnode = lastnode.next;
		}
		return null;	
	}
	
	//实现查找链表中特定的某个节点下一个节点的数据为value并且返回该节点
    public  Node searchPrevious(int value){ 
        Node lastnode = head;
        while(lastnode.next!=null){
            if(lastnode.next.val==value)
                return lastnode;
            lastnode = lastnode.next;
        }
        return null;
    }
	
	//更改链表
	public void changeValue(int value1, int value2) {
		if(search(value1) != null) {
			search(value1).val = value2;
		}
	}
	
	//删除链表中的某个结点
	public void delete(int value) {
		if(search(value) != null) {
			searchPrevious(value).next = search(value).next;
		}
	}
	
	//打印链表
	public void printList() {
		Node cur = head;
		while(cur != null) {
			System.out.println(cur.val);
			cur = cur.next;
		}
	}
	
	public static void main(String[] args) {
		MyLinkedList myLinkedList = new MyLinkedList();
		myLinkedList.addNode(1);
		myLinkedList.addNode(2);
		myLinkedList.addNode(3);
		myLinkedList.addNode(4);
		myLinkedList.addNode(5);
		myLinkedList.changeValue(3, 30);
		myLinkedList.delete(4);
		myLinkedList.printList();
	}
	
}
```

**循环链表**
```java
package Day1;

public class MyCircularLinkedList {
	Node head = null;	//链表头结点
	class Node{
		int val;
		Node next;
		public int getValue() {
			return val;
		}
		
		public void setValue(int value) {
			this.val = value;
		}
		
		public Node getNextNode() {
			return next;
		}
		
		public void setNextNode(Node next) {
			this.next = next;
		}
		
		public Node(int val) {
			// TODO Auto-generated constructor stub
			this.next = null;
			this.val = val;
		}
	}
	
	public static void getNodes(Node startNode) {
		//循环遍历
		Node node = startNode;
		while (node.getNextNode() != startNode.getNextNode()) {
			System.out.println(node.getValue());
			node = node.next;
		}
	}
	
	public static void main(String[] args) {
		MyCircularLinkedList myCircularLinkedList = new MyCircularLinkedList();
		Node node1 = myCircularLinkedList.new Node(1);
        Node node2 = myCircularLinkedList.new Node(2);
        Node node3 = myCircularLinkedList.new Node(3);
        Node node4 = myCircularLinkedList.new Node(4);
        Node node5 = myCircularLinkedList.new Node(5);

        node1.setNextNode(node2);
        node2.setNextNode(node3);
        node3.setNextNode(node4);
        node4.setNextNode(node5);
        node5.setNextNode(node1);

        // getNodes(node1);

        // 添加node6
        Node node6 = myCircularLinkedList.new Node(6);
        node6.setNextNode(node2.getNextNode());
        node2.setNextNode(node6);
        // getNodes(node1);

        // 删除节点
        node2.setNextNode(node3);
        getNodes(node2);

    }
}
```

