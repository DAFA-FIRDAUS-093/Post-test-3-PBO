-----------------------------SISTEM TRAVEL MOBIL ANTAR KOTA KALTIM-------------------------------

1. Judul & Deskripsi Singkat Program

      -  Nama program: Sistem Travel Mobil Antar Kota Kaltim

      -  Deskripsi: Program Java berbasis console untuk mengelola data travel (CRUD: Create, Read, Update, Delete).

2. Struktur Project / Packages (MVC)

      -  main → berisi class main.java (entry point aplikasi)
      
      -  model → berisi class Travel.java (superclass), EkonomiTravel.java, PremiumTravel.java
      
      -  service → berisi class service.java (CRUD logic)
      
      -  Fitur Program
      
      -  Tambah data travel
      
      -  Lihat daftar travel
      
      -  Update data travel
      
      -  Hapus data travel
      
      -  Validasi input (contoh: sopir tidak boleh kosong)
      
      -  Pilihan kategori Ekonomi / Premium dengan konsep inheritance

3. Penerapan Konsep OOP

      -  Encapsulation → Atribut Travel dibuat private dengan getter & setter.

      -  Inheritance → Class EkonomiTravel & PremiumTravel mewarisi Travel.

      -  Polymorphism & Overriding → Method toString() dioverride di subclass untuk menampilkan kategori.

4. Cara Menjalankan Program

      -  Clone repository

      -  Buka di NetBeans / IntelliJ / Eclipse

      -  Jalankan main.java

      -  Ikuti menu console
  
5. Contoh Output Program

   <img width="413" height="218" alt="image" src="https://github.com/user-attachments/assets/d8972fc0-8262-4d5e-883b-9895da10c4e2" />


   Hasilnya:

   <img width="579" height="202" alt="image" src="https://github.com/user-attachments/assets/6446f821-4470-42a6-9b44-b863e6a75e4c" />



6. Kode Program di main.java:

            import java.util.Scanner;
            import model.*;
            import service.service;
            import model.EkonomiTravel;
            import model.PremiumTravel;
            
            
            public class main {
                public static void main(String[] args) {
                    Scanner input = new Scanner(System.in);
                    service service = new service();
                    boolean jalan = true;
            
                    while (jalan) {
                        System.out.println("SISTEM TRAVEL MOBIL ANTAR KOTA KALTIM");
                        System.out.println("1. Tambah Data Travel");
                        System.out.println("2. Lihat Semua Data Travel");
                        System.out.println("3. Update Data Travel");
                        System.out.println("4. Hapus Data Travel");
                        System.out.println("5. Keluar");
                        System.out.print("Pilih menu: ");
                        int pilih = input.nextInt();
                        input.nextLine();
            
                        switch (pilih) {
                            case 1:
                                System.out.print("Nama Sopir: ");
                                String sopir = input.nextLine();
                                System.out.print("Sedang diKota Mana: ");
                                String asal = input.nextLine();
                                System.out.print("Kota Tujuan: ");
                                String tujuan = input.nextLine();
                                System.out.print("Tipe Mobil: ");
                                String tipe = input.nextLine();
            
                                System.out.print("Pilih kategori (1 = Ekonomi, 2 = Premium): ");
                                int kategori = input.nextInt();
                                input.nextLine();
            
                                Travel t;
                                if (kategori == 1) {
                                    t = new EkonomiTravel(sopir, asal, tujuan, tipe);
                                } else {
                                    t = new PremiumTravel(sopir, asal, tujuan, tipe);
                                }
            
                                service.tambahTravel(t);
                                break;
            
                            case 2:
                                service.lihatTravel();
                                break;
            
                            case 3:
                                service.lihatTravel();
                                System.out.print("Pilih nomor data yang ingin diupdate: ");
                                int idxUpdate = input.nextInt() - 1;
                                input.nextLine();
            
                                System.out.print("Nama Sopir baru: ");
                                sopir = input.nextLine();
                                System.out.print("Asal baru: ");
                                asal = input.nextLine();
                                System.out.print("Tujuan baru: ");
                                tujuan = input.nextLine();
                                System.out.print("Tipe Mobil baru: ");
                                tipe = input.nextLine();
            
                                Travel travelBaru = new Travel(sopir, asal, tujuan, tipe);
                                service.updateTravel(idxUpdate, travelBaru);
                                break;
            
                            case 4:
                                service.lihatTravel();
                                System.out.print("Pilih nomor data yang ingin dihapus: ");
                                int idxHapus = input.nextInt() - 1;
                                input.nextLine();
                                service.hapusTravel(idxHapus);
                                break;
            
                            case 5:
                                jalan = false;
                                System.out.println("Terima kasih!");
                                break;
            
                            default:
                                System.out.println("Pilihan tidak valid!");
                        }
                    }
                }
            }
   



7.Kode program di Travel.java:

      public class Travel {
          private String sopir;
          private String asal;
          private String tujuan;
          private String tipeMobil;
      
          // Constructor
          public Travel(String sopir, String asal, String tujuan, String tipeMobil) {
              this.sopir = sopir;
              this.asal = asal;
              this.tujuan = tujuan;
              this.tipeMobil = tipeMobil;
          }
      
          // Getter & Setter
          public String getSopir() {
              return sopir;
          }
      
          public void setSopir(String sopir) {
              this.sopir = sopir;
          }
      
          public String getAsal() {
              return asal;
          }
      
          public void setAsal(String asal) {
              this.asal = asal;
          }
      
          public String getTujuan() {
              return tujuan;
          }
      
          public void setTujuan(String tujuan) {
              this.tujuan = tujuan;
          }
      
          public String getTipeMobil() {
              return tipeMobil;
          }
      
          public void setTipeMobil(String tipeMobil) {
              this.tipeMobil = tipeMobil;
          }
      
          @Override
          public String toString() {
              return "Sopir: " + sopir + ", Asal: " + asal + ", Tujuan: " + tujuan + ", Tipe Mobil: " + tipeMobil;
          }
      }



 8. Kode program di service.java:

            import java.util.ArrayList;
            import model.Travel;
            
            public class service {
                private ArrayList<Travel> daftarTravel = new ArrayList<>();
            
                public void tambahTravel(Travel travel) {
                    daftarTravel.add(travel);
                    System.out.println("Data berhasil ditambahkan!");
                }
            
                public void lihatTravel() {
                    if (daftarTravel.isEmpty()) {
                        System.out.println("Belum ada data travel.");
                    } else {
                        System.out.println("DAFTAR TRAVEL:");
                        for (int i = 0; i < daftarTravel.size(); i++) {
                            System.out.println((i + 1) + ". " + daftarTravel.get(i));
                        }
                    }
                }
            
                public void updateTravel(int index, Travel travelBaru) {
                    if (index >= 0 && index < daftarTravel.size()) {
                        daftarTravel.set(index, travelBaru);
                        System.out.println("Data berhasil diupdate!");
                    } else {
                        System.out.println("Data tidak ditemukan.");
                    }
                }
            
                public void hapusTravel(int index) {
                    if (index >= 0 && index < daftarTravel.size()) {
                        daftarTravel.remove(index);
                        System.out.println("Data berhasil dihapus!");
                    } else {
                        System.out.println("Data tidak ditemukan.");
                    }
                }
            }



9.Kode program di EkonomiTravel:

      public class EkonomiTravel extends Travel {
          public EkonomiTravel(String sopir, String asal, String tujuan, String tipeMobil) {
              super(sopir, asal, tujuan, tipeMobil);
          }
      
          @Override
          public String toString() {
              return super.toString() + " (Ekonomi)";
          }
      }



10. Kode program di PremiumTravel:


            public class PremiumTravel extends Travel {
                public PremiumTravel(String sopir, String asal, String tujuan, String tipeMobil) {
                    super(sopir, asal, tujuan, tipeMobil);
                }
            
                @Override
                public String toString() {
                    return super.toString() + " (Premium)";
                }
            }
            


11. kode program bagian Getter dan Setter berada di Travel:

          public String getSopir() {
              return sopir;
          }
      
          public void setSopir(String sopir) {
              this.sopir = sopir;
          }
      
          public String getAsal() {
              return asal;
          }
      
          public void setAsal(String asal) {
              this.asal = asal;
          }
      
          public String getTujuan() {
              return tujuan;
          }
      
          public void setTujuan(String tujuan) {
              this.tujuan = tujuan;
          }
      
          public String getTipeMobil() {
              return tipeMobil;
          }
      
          public void setTipeMobil(String tipeMobil) {
              this.tipeMobil = tipeMobil;
          }
      
          @Override
          public String toString() {
              return "Sopir: " + sopir + ", Asal: " + asal + ", Tujuan: " + tujuan + ", Tipe Mobil: " + tipeMobil;
          }
      }
          
12. Untuk Superclass dan juga subclass

    untuk foldernya:

    <img width="415" height="221" alt="image" src="https://github.com/user-attachments/assets/db4dabe3-4069-4a3c-8fef-b8d55970ee99" />


    Penjelasannya:
    1. Superclass
       - Travel.java
       - Ini adalah kelas induk (superclass)
       - Atribut ini dienkapsulasi (private) lalu diakses lewat getter & setter
       - Class ini juga bisa punya method umum, misalnya toString() untuk menampilkan data.
      
    2. Subcalss
       1. EkonomiTravel.java
          - Ini adalah kelas turunan (subclass) dari Travel.
          - Ditulis dengan extends Travel.
          - Bisa menambahkan atribut khusus, misalnya hargaTiket lebih murah.
          - Bisa override method dari superclass, misalnya toString().
         
       2. PremiumTravel.java
          - Sama, ini juga subclass dari Travel.
          - juga pakai extends Travel.
          - Bisa menambahkan fitur berbeda (misalnya fasilitas lebih lengkap, harga lebih mahal).
          - Bisa override method juga.
