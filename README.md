# Tugas-ASDL-2
Anggota Kelompok 5 : 

Aditiya Kurniawan (09021182126028) Putri Agustina (09021182126029) Eka Wira Yudha (09021182126031) Deva Saumena  (09021182126032) Muhamad Nurhadi (09021182126033).

-#Tugas 2A #-

package DoubleLinkedlist;

import java.util.Scanner;
import java.util.*;

public class DoubleLinkedList {

	public static void main(String[] args) {
		 // TODO Auto-generated method stub
		int data; int data1; int data2; int data3; int a,b,c,d; 
	
		Scanner s = new Scanner (System.in);
		LinkedList<Integer> llist = new LinkedList<>();
		 for(int w = 0; w==(0) || w==(0);){
		System.out.println("|| 1.Operasi Tambah Data       ||");
		System.out.println("|| 2.Operasi Tambah Data Awal  ||");
		System.out.println("|| 3.Operasi Tambah Data Tengah||");
		System.out.println("|| 4.Operasi Tambah Data Akhir ||");
		System.out.println("|| 5.Operasi Hapus Data Awal   ||");
		System.out.println("|| 6.Operasi Hapus Data Tengah ||");
		System.out.println("|| 7.Operasi Hapus Data Akhir  ||");
		System.out.println("Silahkan Pilih Operasi Berdasarkan Nomor [1/2/3/4/5/6/7] = ");
		data = s.nextInt();
		
		
		if (data==1) {
			System.out.println("Masukan data = ");
			a = s.nextInt();
			b = s.nextInt();
			c= s.nextInt();
			llist.add(a);
			llist.add(b);
			llist.add(c);
			System.out.println(llist);

		}
		
		else if (data==2) {
			System.out.println("|~Operasi tambah data awal~|");
			System.out.println("Masukan data = ");
			data1 = s.nextInt();
			llist.addFirst(data1);
			System.out.println(llist);
		}
		
		else if (data==3) {
			System.out.println("|~Operasi tambah data tengah~|");
			System.out.println("Masukan Data = ");
			data2 = s.nextInt();
			llist.add(2, data2); 
			 System.out.println(llist);
		}
		else if (data==4) {
			System.out.println("|~Operasi tambah data akhir~|");
			System.out.println("Masukan data = ");
			data3 = s.nextInt();
			llist.addLast(data3);
			System.out.println(llist);
		}
		else if (data==5) {
			System.out.println("|~Operasi hapus data awal~|");
			llist.removeFirst();
			 System.out.println(llist);
		}
		else if (data==6) {
			System.out.println("|~Operasi hapus data tengah~|");
			llist.remove(2);
			 System.out.println(llist);
		}
		else if (data==7) {
			System.out.println("|~Operasi hapus data akhir~|");
			llist.removeLast(); 
			 System.out.println(llist);
		}
		
		System.out.println("|Input 0 untuk mengulang kembali dan 10 untuk berhenti =  |");
		w = s.nextInt();
		
		
		
		
		 }
	}

}


-# Tugas 2B #-

package DoubleLinkedlist;

import java.util.Scanner;

public class Scan {
 
		  private static Scanner scanner = new Scanner(System.in);
		    
		    public static String stringScn(String message){
		        System.out.print(message + ": " );
		        return scanner.next();
		    }

		    public static int integerScn(String message){
		        System.out.print(message + ": ");
		        return scanner.nextInt();
		    }
		}


package DoubleLinkedlist;

public class doublelinked {

    private int size = 1;

    Node head;
    Node tail;

    static class Node{
        
        int data;
        Node prev;
        Node next;
        int index;

        Node(int d){
            index = 0;
            data = d;
            next = null;
            prev = null;
        }

        Node(){}

    }

    public void printList(boolean asc){
        Node n = null;

        if(asc){
            n = head;
        } else {
            n = tail;
        }

        System.out.print("[ ");

        while(n != null){
            System.out.print(n.data + " ");

            if(asc){
                n = n.next;
            } else {
                n = n.prev;
            }
        }


        System.out.print("]\n");
    }

    public void addFirst(int data, doublelinked dList){
        Node node = new Node(data);
        if(this.head == null){
            dList.head = node;
            head = node;
            head.next = null;
            head.index = 0;
        } else {
            node.next = head;
            node.prev = null;
            head.prev = node;

            head = node;
            increaseSize();
            Node n = head;
            for (int i = 1; i < getSize(); i++) {
                n.next.index = i;
                if(i == getSize()-1){
                    tail = n.next;
                }
                n = n.next;
            }
            
            //head.next.index++;
            // update index
            
        }
    }

    public void add(int index, int data){

        Node node = searchNodeByIndex(index);

        Node newNode = new Node(data);
        increaseSize();
        node.prev.next = newNode;
        newNode.prev = node.prev;
        newNode.next = node;
        if(newNode.next != null){
            newNode.next.prev = newNode;
            Node n = newNode;
            n.index = index;
            for (int i = (index + 1); i < getSize(); i++) {
                n.next.index = i;
                n = n.next;
            }
        }
    }

    public void addLast(int data){
        Node n = head;
        while(n.next != null){
            n = n.next;
        }

        Node lastNode = new Node(data);
        increaseSize();
        n.next = lastNode;
        lastNode.prev = n;
        //n = lastNode;
        tail = lastNode;
        tail.index = getSize() - 1;
    }

    public void removeFirst(){
        Node n = head.next;
        head = null;
        head = n;
        decreaseSize();

        Node node = head;
        for (int i = 0; i < getSize(); i++) {
            node.index = i;
            node = node.next;
        }
    }

    public void remove(int index){
        Node target = searchNodeByIndex(index);
        Node n = head;
        while(n.next != null){
            if(n.next == target){
                n.next = target.next;
                target.next.prev = n;
                decreaseSize();
                n = target.next;
                for (int i = index; i < getSize(); i++) {
                    n.index = i;
                    n = n.next;
                }
                break;
            }
            n = n.next;
        }
    }

    public void removeLast(){
        Node n = tail.prev;
        if(n == null){
            head = null;
            decreaseSize();
        } else {
            n.next = null;
            tail = n;
            decreaseSize();
        }
    }

    public void setData(int index, int element){
        try {
            Node n = searchNodeByIndex(index);
            n.data = element;
            System.out.println("Data berhasil diubah");
        } catch (Exception e) {
            System.err.println("Data tidak ditemukan");
        }
    }

    public boolean searchByData(int element){
        Node n = head;

        while(n != null){ 
            if(n.data == element){
                return true;
            }   
            n = n.next;
        }
        return false;
    }

    public Node searchNodeByIndex(int index){
        Node n = head;

        while(n != null){
            if(n.index == index){
                return n;
            }
            n = n.next;
        }
        return null;
    }

    public int getSize() {
        return this.size;
    }

    public void increaseSize() {
        this.size++;
    }

    public void decreaseSize(){
        this.size--;
    }
}

package DoubleLinkedlist;

import java.util.Scanner;
import java.util.*;

public class DoubleLinkedList {

	public static void main(String[] args) {
		 // TODO Auto-generated method stub
		int data; int data1; int data2; int data3; int a,b,c,d; 
	
		Scanner s = new Scanner (System.in);
		LinkedList<Integer> llist = new LinkedList<>();
		 for(int w = 0; w==(0) || w==(0);){
		System.out.println("|| 1.Operasi Tambah Data       ||");
		System.out.println("|| 2.Operasi Tambah Data Awal  ||");
		System.out.println("|| 3.Operasi Tambah Data Tengah||");
		System.out.println("|| 4.Operasi Tambah Data Akhir ||");
		System.out.println("|| 5.Operasi Hapus Data Awal   ||");
		System.out.println("|| 6.Operasi Hapus Data Tengah ||");
		System.out.println("|| 7.Operasi Hapus Data Akhir  ||");
		System.out.println("Silahkan Pilih Operasi Berdasarkan Nomor [1/2/3/4/5/6/7] = ");
		data = s.nextInt();
		
		
		if (data==1) {
			System.out.println("Masukan data = ");
			a = s.nextInt();
			b = s.nextInt();
			c= s.nextInt();
			llist.add(a);
			llist.add(b);
			llist.add(c);
			System.out.println(llist);

		}
		
		else if (data==2) {
			System.out.println("|~Operasi tambah data awal~|");
			System.out.println("Masukan data = ");
			data1 = s.nextInt();
			llist.addFirst(data1);
			System.out.println(llist);
		}
		
		else if (data==3) {
			System.out.println("|~Operasi tambah data tengah~|");
			System.out.println("Masukan Data = ");
			data2 = s.nextInt();
			llist.add(2, data2); 
			 System.out.println(llist);
		}
		else if (data==4) {
			System.out.println("|~Operasi tambah data akhir~|");
			System.out.println("Masukan data = ");
			data3 = s.nextInt();
			llist.addLast(data3);
			System.out.println(llist);
		}
		else if (data==5) {
			System.out.println("|~Operasi hapus data awal~|");
			llist.removeFirst();
			 System.out.println(llist);
		}
		else if (data==6) {
			System.out.println("|~Operasi hapus data tengah~|");
			llist.remove(2);
			 System.out.println(llist);
		}
		else if (data==7) {
			System.out.println("|~Operasi hapus data akhir~|");
			llist.removeLast(); 
			 System.out.println(llist);
		}
		
		System.out.println("|Input 0 untuk mengulang kembali dan 10 untuk berhenti =  |");
		w = s.nextInt();
		
		
		
		
		 }
	}

}










