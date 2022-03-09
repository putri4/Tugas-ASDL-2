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

import java.util.LinkedList;

public class Linkedlist {

    static int option;
    static boolean isContinue;

    private static boolean isManual;

    public static LinkedList<Integer> list = new LinkedList<Integer>();
    public static doublelinked dList = new doublelinked();

    public static void main(String[] args) {
        menuUtama();
    }

    public static void menuUtama() {
        System.out.println("*** DOUBLE LINKED LIST ***");
        System.out.println("    1. Manual");
        System.out.println("    2. Pustaka");
        System.out.println("    3. Keluar");
        option = Scan.integerScn("    Silakan pilih [1/2/3]");

        switch (option) {
            /**
             * di opsi ini akan ditentukan apakah program menyimpan data di double linked list manual atau library
             * ketika case 1 terpilih maka, method setIsManual akan menyimpan value true di variable isManual(boolean)
             * begitupun sebaliknya untuk case 2
             * 
             * ketika variable isManual sudah memiliki value (true atau false) maka variable ini bisa dimanfaatkan untuk method lainnya
             * baca line 208
             */
            case 1:
                setIsManual(true);
                pilihanOperasi();
                break;
            case 2:
                setIsManual(false);
                pilihanOperasi();
                break;
            case 3:
                break;
            default:
                System.out.println("pilihan tidak diketahui");
        }
    }

    public static void pilihanOperasi() {
        isContinue = true;
        option = 0;

        System.out.println("*** OPERASI DOUBLE LINKED LIST ***");
        System.out.println("    1. Tambah Data");
        System.out.println("    2. Hapus Data");
        System.out.println("    3. Pencarian/Pengubahan Data");
        System.out.println("    4. Kembali");

        while (isContinue) {
            option = Scan.integerScn("    Silakan pilih [1/2/3/4]");

            switch (option) {
                case 1:
                    isContinue = false;
                    tambahDataMenu();
                    break;
                case 2:
                    isContinue = false;
                    hapusDataMenu();
                    break;
                case 3:
                    isContinue = false;
                    ubahDataMenu();
                    break;
                case 4:
                    isContinue = false;
                    menuUtama();
                    break;
                default:
                    isContinue = true;
            }
        }

    }

    public static void tambahDataMenu() {
        // 1. Tambah Data
        isContinue = true;
        option = 0;

        System.out.println("*** OPERASI TAMBAH DATA DOUBLE LINKED LIST ***");
        System.out.println("    1. Tambah Data Awal");
        System.out.println("    2. Tambah Data Tengah");
        System.out.println("    3. Tambah Data Akhir");
        System.out.println("    4. Cetak Data");
        System.out.println("    5. Kembali");

        while (isContinue) {
            option = Scan.integerScn("Silakan pilih [1/2/3/4/5]");

            switch (option) {
                case 1:
                    isContinue = false;
                    tambahDataAwalView();
                    break;
                case 2:
                    isContinue = false;
                    tambahDataTengahView();
                    break;
                case 3:
                    isContinue = false;
                    tambahDataAkhirView();
                    break;
                case 4:
                    isContinue = false;
                    cetakData(1); // true karena menu tambah data
                    break;
                case 5:
                    isContinue = false;
                    pilihanOperasi();
                    break;
                default :
                    isContinue = true;
            }

        }

    }

    public static void hapusDataMenu(){
        // 2. Hapus data

        isContinue = true;
        option = 0;

        System.out.println("*** OPERASI HAPUS DATA DOUBLE LINKED LIST ***");
        System.out.println("    1. Hapus Data Awal");
        System.out.println("    2. Hapus Data Tengah");
        System.out.println("    3. Hapus Data Akhir");
        System.out.println("    4. Cetak Data");
        System.out.println("    5. Kembali");

        while (isContinue) {
            option = Scan.integerScn("Silakan pilih [1/2/3/4/5]");

            switch (option) {
                case 1:
                    isContinue = false;
                    hapusDataAwalView();
                    break;
                case 2:
                    isContinue = false;
                    hapusDataTengahView();
                    break;
                case 3:
                    isContinue = false;
                    hapusDataAkhirView();
                    break;
                case 4:
                    isContinue = false;
                    cetakData(2); // false karena bukan menu tambah data
                    break;
                case 5:
                    isContinue = false;
                    pilihanOperasi();
                    break;
                default :
                    isContinue = true;
            }

        }

    }

    public static void ubahDataMenu(){
        // 3. Ubah data dan cari data
        
        isContinue = true;
        option = 0;
        
        System.out.println("*** OPERASI PENCARIAN/PENGUBAHAN DATA DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    1. Cari data");
        System.out.println("    2. Ubah data");
        System.out.println("    3. Cetak data");
        System.out.println("    4. Kembali");
        option = Scan.integerScn("    Silakan pilih [1/2/3/4]");

        switch(option){
            case 1 : 
                isContinue = false;
                cariDataView();
                break;
            case 2 :
                isContinue = false;
                ubahDataView();                
                break;
            case 3 :
                isContinue = false;
                cetakData(3);;
                break;
            case 4 :
                isContinue = false;
                pilihanOperasi();
                break;
            default :
                isContinue = true;
        }

    }

    /**
     * TAMBAH DATA
     */

    public static void tambahDataAwalView(){
        isContinue = true;
        String element;
        int index = 1;

        System.out.println("*** OPERASI TAMBAH DATA AWAL DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    INFO: - Masukan data angka (integer)");
        System.out.println("          - Ketik 'stop' untuk kembali ke menu sebelumnya");
        System.out.println();
        
        while(isContinue){
            element = Scan.stringScn("Data ke-" + index);

            char[] chars = element.toCharArray();
            if(Character.isDigit(chars[0])){
                tambahDataAwal(Integer.parseInt(element));
                index++;
            } else {
                if(!element.equals("stop")){
                    // Jika user tidak memasukan kata "stop" maka loop tetap berlangsung
                    isContinue = true;
                } else {
                    // loop  berhenti karena user memasukan kata "stop"
                    isContinue = false;
                    tambahDataMenu();
                }
            }
        }
    }

    public static void tambahDataAwal(int element) {
        // 1. Tambah data awal

        /**
         * Ini merupakan salah satu method yang memanfaatkan variable isManual
         * dengan menggunakan method getIsmanual() maka kita bisa mengambil value dari varible isManual
         * 
         * bisa diperhatikan perkondisian dibawah, ketika isManual bervalue true maka program akan menginstruksikan untuk menyimpan data
         * menggunakan double linked list manual
         * 
         * jika isManual bervalue false maka data akan disimpan menggunakan double linked list library
         */
        if(getIsManual()){
            // Manual
            dList.addFirst(element, dList);
        } else if(!getIsManual()) {
            // Pustaka
            list.addFirst(element);
        }
    }

    /**
     * TAMBAH DATA TENGAH
     */

    public static void tambahDataTengahView(){
        int index, element;
        isContinue = true;
        System.out.println("*** OPERASI TAMBAH DATA TENGAH DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    INFO: - Masukan index angka (integer)");
        System.out.println("          - Masukan data angka (integer)");
        
        index = Scan.integerScn("Index ke-");
        element = Scan.integerScn("Masukan data");
        
        tambahDataTengah(index, element);
        // mengecek bagaimana jika index yang dimasukan belum ada
        System.out.print("Tekan Enter untuk melanjutkan");
        try {System.in.read();} 
        catch (Exception e) {}
        tambahDataMenu();
    }

    public static void tambahDataTengah(int index, int element) {
        // 2. Tambah data tengah
        if(getIsManual()){
            // Manual
            dList.add(index, element);
        } else if(!getIsManual()) {
            // Pustaka
            list.add(index, element);
        }
    }

    /**
     * TAMBAH DATA AKHIR
     */

    public static void tambahDataAkhirView(){
        String element;
        isContinue = true;
        
        System.out.println("*** OPERASI TAMBAH DATA AKHIR DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    INFO - Masukan data angka (integer)");
        System.out.println();

        while(isContinue){
            element = Scan.stringScn("Data");

            char[] chars = element.toCharArray();
            if(Character.isDigit(chars[0])){
                tambahDataAwal(Integer.parseInt(element));
            } else {
                if(!element.equals("stop")){
                    // Jika user tidak memasukan kata "stop" maka loop tetap berlangsung
                    isContinue = true;
                } else {
                    // loop  berhenti karena user memasukan kata "stop"
                    isContinue = false;
                    tambahDataMenu();
                }
            }
        }
    }

    public static void tambahDataAkhir(int element) {
        // 3. Tambah data akhir
        if(getIsManual()){
            // Manual
            dList.addLast(element);
        } else if(!getIsManual()) {
            // Pustaka

            list.addLast(element);

        }
    }

    /**
     * HAPUS DATA
     */

    public static void hapusDataAwalView(){
        isContinue = true;
        String argument;

        System.out.println("*** OPERASI HAPUS DATA AWAL DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    INFO - Ketik yes (enter) untuk menghapus data");
        System.out.println();
        
        while(isContinue){
            argument = Scan.stringScn("Anda yakin ingin menghapus data di awal? ");
            if(argument.equalsIgnoreCase("yes")){
                hapusDataAwal();
                isContinue = false;
                System.out.print("Tekan Enter untuk melanjutkan");
                try{System.in.read();}
                catch(Exception e){}
                hapusDataMenu();
            } else if (argument.equalsIgnoreCase("no")){
                hapusDataMenu();
                isContinue = false;
            } else {
                isContinue = true;
            }
        }

    }

    public static void hapusDataAwal() {
        // 1. Hapus Data awal
        if(getIsManual()){
            // Manual
            dList.removeFirst();
        } else if(!getIsManual()) {
            // Pustaka
            list.removeFirst();
        }
    }
    
    /**
     * HAPUS DATA TENGAH
     */

    public static void hapusDataTengahView(){
        int index;
        String argument;

        System.out.println("*** OPERASI HAPUS DATA TENGAH DOUBLE LINKED LIST");
        System.out.println();
        System.out.println("    INFO - Masukan index angka (integer) data yang ingin di hapus");
        System.out.println("         - Ketik yes (enter) untuk menghapus data");
        System.out.println();

        index = Scan.integerScn("Data ke (index)");
        
        argument = Scan.stringScn("Anda yakin ingin menghapus data di index ke-" + index);
        if(argument.equalsIgnoreCase("yes")){
            hapusDataTengah(index);
        }
        System.out.print("Tekan Enter untuk melanjutkan");
        try{System.in.read();}
        catch(Exception e){}

        hapusDataMenu();
    }

    public static void hapusDataTengah(int index) {
        // 2. Hapus data tengah
        if(getIsManual()){
            // Manual
            dList.remove(index);
        } else if(!getIsManual()) {
            // Pustaka
            list.remove(index);
        }
    }

    /**
     * HAPUS DATA AKHIR
     */

    public static void hapusDataAkhirView(){
        String argument;
        
        System.out.println("*** OPERASI HAPUS DATA AKHIR DOUBLE LINKED LIST ***");
        System.out.println();
        System.out.println("    INFO - Ketik yes (enter) untuk menghapus data");
        System.out.println();
        argument = Scan.stringScn("Yakin ingin menghapus data akhir? ");
        if(argument.equalsIgnoreCase("yes")){
            hapusDataAkhir();
        }
        System.out.print("Tekan Enter untuk lanjutkan");
        try{System.in.read();}
        catch(Exception e){}

        hapusDataMenu();
    }

    public static void hapusDataAkhir() {
        // 3. Hapus data akhir
        if(getIsManual()){
            // Manual
            dList.removeLast();
        } else if(!getIsManual()) {
            // Pustaka
            list.removeLast();
        }
    }
    
    /**
     * UBAH DATA
     */

    public static void ubahDataView(){
        int index, element;
        
        System.out.println("*** OPERASI UBAH DATA ***");
        System.out.println();
        System.out.println("    INFO - Masukan index angka (Integer)");
        System.out.println("         - Masukan data yang diubah berupa angka (Integer)");
        System.out.println();
        
        index = Scan.integerScn("Index");
        element = Scan.integerScn("Data");

        ubahData(index, element);

        System.out.print("Tekan Enter untuk melanjutkan");
        try{System.in.read();}
        catch(Exception e){}
        ubahDataMenu();
    }
    
    public static void ubahData(int index, int element) {
        // 4. Ubah data
        if(getIsManual()){
            dList.setData(index, element);
        } else if(!getIsManual()){
            list.set(index, element);
        }
    }
    
    /**
     * CARI DATA
     */

    public static void cariDataView(){
        int element;
        
        System.out.println("*** OPERASI CARI DATA ***");
        System.out.println();
        System.out.println("    INFO - Masukan data yang ingin dicari berupa angka (Integer)");
        System.out.println();

        element = Scan.integerScn("Data");

        if(cariData(element)){
            System.out.println("Data ditemukan");
        } else {
            System.out.println("Data tidak ditemukan");
        }
        
        System.out.print("Tekan Enter untuk melanjutkan");
        try{System.in.read();}
        catch(Exception e){}
        ubahDataMenu();
    }

    public static boolean cariData(int element){
        
        if(dList.searchByData(element)){
            return true;
        } else {
            return false;
        }
    }

    public static void cetakData(int key){
        if(getIsManual()){
            System.out.println("*** CETAK DATA DOUBLE LINKED LIST ***");
            System.out.println();
            System.out.print("    "); dList.printList(true);
            System.out.println();
            System.out.print("Tekan Enter untuk melanjutkan");
            try{System.in.read();}
            catch(Exception e){}
            if(key == 1){
                tambahDataMenu();
            } else if (key == 2){
                hapusDataMenu();
            } else if(key == 3){
                ubahDataMenu();
            }
        } else if(!getIsManual()){
            System.out.println("*** CETAK DATA DOUBLE LINKED LIST ***");
            System.out.println();
            System.out.println("    " + list);
            System.out.println();
            System.out.print("Tekan Enter untuk melanjutkan");
            try{System.in.read();}
            catch(Exception e){}
            if(key == 1){
                tambahDataMenu();
            } else if(key == 2){
                hapusDataMenu();
            } else if(key == 3){
                ubahDataMenu();
            }
        }
    }

    public static void setIsManual(boolean manual){
        isManual = manual;
    }

    public static boolean getIsManual(){
        return isManual;
    }
}











