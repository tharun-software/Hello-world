
<!-- linked list datastructure-->

package DataStructure;

public class LinkedList_Implementation {

	Node head;
	int size;

	class Node {
		private Object value;
		private Node next;

		Node(Object recievdValue) {
			this.value = recievdValue;
			this.next = null;
		}

		public Object getValue() {
			return value;
		}

		public void setValue(Object value) {
			this.value = value;
		}

		public Node getNext() {
			return next;
		}

		public void setNext(Node next) {
			this.next = next;
		}

	}

	// linear search
	public boolean linearSearch(Node head, Object elementToFind) {
		Node current = head; // starts with the head(first element)
		while (current != null) {

			if (current.value == elementToFind) {
				return true;
			} else {
				current = current.next;
			}

		}
		return false;
	}

	// 17
	public void addFirst(Object newValue) {
		Node newNode = new Node(newValue); // adding value will pass to node class constructor
		if (head == null) {
			head = newNode; // if head is null "upcoming new node becomes head "
		} else {
			newNode.next = head; // if head is not null then head becomes next elemt of new node.
			head = newNode;// then new node becomes head;
		}
		size++; // increase the total number of elemnts
	}

	public void addLast(Object newValue) {

		Node newNode = new Node(newValue);

		if (head == null) {
			head = newNode;
		} else {
			Node current = head;
			while (current.next != null) {
				current = current.next;

			}
			current.next = newNode;

		}
		size++;
	}

	public boolean addMiddle(int index, Object newValue) {
		if (index < 0 || index > size) {
			// this check just for index is placed inside first and last node

			return false;

		}
		Node newNode = new Node(newValue);
		Node current = head;
		Node previous = null; // previus is null at begining

		for (int i = 0; i < index; i++) {

			previous = current;
			current = current.next;

		}
		if (current == null) {
			// if cuurent is null then the previous is the last elemnts
			// then previous.next =new node or new value is the next value of previus one
			previous.next = newNode;
		} else {
			if (current == head) {
//if current is head then we r inserting the new value in the beginning itself of the list.like add first
//changing head because inserting at first
				newNode.next = head;
				head = newNode;
			} else {

				// this part iis key part
				// index is not first or last its in the middle so that
// sothat previous.next value is the middle value to be inserted and next value of the newnode is the cuurent value
				previous.next = newNode;
				newNode.next = current;

			}
		}
		size++;
		return true;
	}

	public Node removeFirst() {

		if (size == 0) {
			throw new IllegalStateException();
		}

		Node toRemove = head;
		head = head.next; //the second elemnt becomes head element
		toRemove.next = null;

		return head;

	}

	public Object get(int index) {
		if (index < 0 || index >= size) {
			return null;
		}
		Node current = head;
		for (int i = 0; i < index; i++) {
			current = current.next;
		}

		return current.value;

	}

	public static void main(String[] args) {
		LinkedList_Implementation list = new LinkedList_Implementation();
		// 43 => 56 => 86 => 45 => 32 =>17
		list.addFirst(17);
		list.addFirst(32);
		list.addFirst(45);
		list.addFirst(86);
		list.addFirst(56);
		list.addFirst(43);
		for (int i = 0; i < list.size; i++) {
			System.err.println(list.get(i));
		}

		list.addMiddle(2, 33);
		System.err.println("");

		for (int i = 0; i < list.size; i++) {
			System.err.println(list.get(i));
		}

	}

}
