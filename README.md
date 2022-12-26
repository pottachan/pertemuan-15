import java.sql.*;
import java.util.Scanner;
public class masukdata {
	public static void koneksi() {
		try {
			Connection conn = null;
			conn = DriverManager.getConnection("jdbc:sqlite:C:/pemrograman3/toko.sql");
		System.out.println("Terkoneksi");
		}catch (SQLException e) {
			System.out.println(e.getMessage());
		}
	}
	public static void masuk() {
try {
	String a, b, sql;
	int c, d;
	Connection conn = null;
	conn = DriverManager.getConnection("jdbc:sqlite:C:/pemrograman3/toko.sql");
	Scanner sc = new Scanner(System.in);
	System.out.print("Masukan Kode Barang : ");
	a = sc.nextLine();
	System.out.print("Masukan Nama Barang : ");
	b = sc.nextLine();
	System.out.print("Masukan Jumlah Barang : ");
	c = sc.nextInt();
	System.out.print("Masukan Harga Satuan :");
	d = sc.nextInt();
	sql = "insert into barang values ('"+a+"','"+b+"','"+c+"','"+d+"')";
	PreparedStatement st = conn.prepareStatement(sql);
	st.execute();
	System.out.println("");
	System.out.println("Data berhasil masuk");
	System.out.println("");
	lihat();
	conn.close();
	sc.close();
}catch (SQLException e) {
	System.out.println(e.getMessage());
}
	}
	public static void lihat() {
try {
	Connection conn = null;
	String sql = "Select * from barang";
	conn = DriverManager.getConnection("jdbc:sqlite:C:/pemrograman3/toko.sql");
	Statement st = conn.createStatement();
	ResultSet rs = st.executeQuery(sql);
	System.out.println("=======================================================");
	System.out.println("Kode\tNama Barang\t\tJumlah Barang\tHarga Satuan ");
	System.out.println("=======================================================");
	while(rs.next()) {
		System.out.print(rs.getString("kode"));
		System.out.print("\t\t"+rs.getString("nmbarang"));
		System.out.print("\t\t\t\t    "+rs.getInt("qty"));
		System.out.println("\t\t\t"+rs.getInt("harga"));
	}
	st.close();
	conn.close();
}catch(Exception e) {
	System.out.println(e.getMessage());
}
	}
public static void hapus() {
	try {
		String h, sql;
		Connection conn = null;
		conn = DriverManager.getConnection("jdbc:sqlite:C:/pemrograman3/toko.sql");
		Statement st = conn.createStatement();
		Scanner sc = new Scanner(System.in);
		System.out.println("Hapus Record...");
		System.out.print("Kode Barang : ");
		h = sc.nextLine();
		sql = "delete from barang where kode='"+h+"'";
		st.execute(sql);
		System.out.println("");
		System.out.println("Data berhasil dihapus\n");
		lihat();
		st.close();
		conn.close();
		sc.close();
	}catch(Exception e) {
		System.out.println(e.getMessage());
	}
}
public static void ubah() {
try {
	String k,sql; 
	int j, h;
	Connection conn = null;
	conn = DriverManager.getConnection("jdbc:sqlite:C:/pemrograman3/toko.sql");
	Scanner sc = new Scanner(System.in);
	System.out.println("Ubah record....");
	System.out.print("Masukan kode barang : ");
	k = sc.nextLine();
	System.out.print("Masukan jumlah barang : ");
	j = sc.nextInt();
	System.out.print("Masukan harga barang : ");
	h = sc.nextInt();
	sql = "update barang set qty='"+j+"', harga='"+h+"' where kode='"+k+"'";
	PreparedStatement st = conn.prepareStatement(sql);
	st.executeUpdate();
	lihat();
	sc.close();
	st.close();
	conn.close();
	}catch(Exception e) {
	System.out.println(e.getMessage());
}
}
	public static void main(String[] args) {
		balik:{
		int pil;
		System.out.println("=======================================");
		System.out.println("\t\t\t\t Kopindra ");
		System.out.println("=======================================");
		System.out.println("1. Memasukan Data Barang");
		System.out.println("2. Mengubah Data Barang");
		System.out.println("3. Menghapus Data Barang");
		System.out.println("4. Melihat Data Barang");
		System.out.println("=======================================");
		Scanner sc = new Scanner(System.in);
		System.out.print("Masukan(angka) pilihan anda : ");
		pil = sc.nextInt();
		switch(pil) {
		case 1:
			System.out.println("\n");
			masuk();
			break;
		case 2:
			System.out.println("\n");
			ubah();
			break;
		case 3:
			System.out.println("\n");
			hapus();
			break;
		case 4:
			System.out.println("\n");
			lihat();
			break balik;
		default:
			System.out.println("anda belum memilih");
			break;
		}
		}
		}
	}


