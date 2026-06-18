package main
import "fmt"
const NMAX int = 100
type Task struct {
	Nama         string
	Ruangan      string
	Kesulitan    int
	Durasi       int
	SudahSelesai bool
}
type tabTask [NMAX]Task
func inisialisasiData(A *tabTask, n *int) {

	(*A)[0] = Task{"Menyapu", "RuangTamu", 2, 15, true}
	(*A)[1] = Task{"Mengepel", "Kamar", 3, 20, false}
	(*A)[2] = Task{"Mencuci", "Dapur", 4, 30, true}

	*n = 3
}
func tambahTugas(A *tabTask, n *int) {

	fmt.Println("\n=== TAMBAH TUGAS ===")

	fmt.Print("Nama : ")
	fmt.Scan(&(*A)[*n].Nama)

	fmt.Print("Ruangan : ")
	fmt.Scan(&(*A)[*n].Ruangan)

	fmt.Print("Kesulitan : ")
	fmt.Scan(&(*A)[*n].Kesulitan)

	fmt.Print("Durasi : ")
	fmt.Scan(&(*A)[*n].Durasi)

	fmt.Print("Status selesai (true/false) : ")
	fmt.Scan(&(*A)[*n].SudahSelesai)

	*n = *n + 1

	fmt.Println("Data berhasil ditambah")
}
func tampilkanTugas(A tabTask, n int) {

	var i int
	var status string

	fmt.Println("\n=== DAFTAR TUGAS ===")
	//mengunjungi setiap index
	for i = 0; i < n; i++ {
		//mengecek status tugas
		if A[i].SudahSelesai {
			status = "Selesai"
		} else {
			status = "Belum"
		}

		fmt.Println("---------------------------")
		fmt.Println("Index      :", i)
		fmt.Println("Nama       :", A[i].Nama)
		fmt.Println("Ruangan    :", A[i].Ruangan)
		fmt.Println("Kesulitan  :", A[i].Kesulitan)
		fmt.Println("Durasi     :", A[i].Durasi, "menit")
		fmt.Println("Status     :", status)
	}
}
func ubahTugas(A *tabTask, n int) {

	var idx int

	tampilkanTugas(*A, n)

	fmt.Print("\nMasukkan index yang ingin diubah : ")
	fmt.Scan(&idx)

	if idx >= 0 && idx < n {

		fmt.Print("Nama baru : ")
		fmt.Scan(&(*A)[idx].Nama)

		fmt.Print("Ruangan baru : ")
		fmt.Scan(&(*A)[idx].Ruangan)

		fmt.Print("Kesulitan baru : ")
		fmt.Scan(&(*A)[idx].Kesulitan)

		fmt.Print("Durasi baru : ")
		fmt.Scan(&(*A)[idx].Durasi)

		fmt.Print("Status selesai : ")
		fmt.Scan(&(*A)[idx].SudahSelesai)

		fmt.Println("Data berhasil diubah")

	} else {

		fmt.Println("Index tidak valid")
	}
}
func hapusTugas(A *tabTask, n *int) {

	var idx int
	var i int

	tampilkanTugas(*A, *n)

	fmt.Print("\nMasukkan index yang ingin dihapus : ")
	fmt.Scan(&idx)

	if idx >= 0 && idx < *n {
		//menggeser data 
		for i = idx; i < *n-1; i++ {

			(*A)[i] = (*A)[i+1]
		}
		//untuk mengurangi datanya 
		*n = *n - 1

		fmt.Println("Data berhasil dihapus")

	} else {

		fmt.Println("Index tidak valid")
	}
}
func sequentialSearchNama(A tabTask, n int) {

	var cari string
	var i int
	var ketemu bool

	fmt.Print("Cari nama tugas : ")
	fmt.Scan(&cari)

	ketemu = false
	// memeriksa semua data
	for i = 0; i < n; i++ {

		if A[i].Nama == cari {

			fmt.Println("\nData ditemukan")
			fmt.Println(A[i])

			ketemu = true
		}
	}

	if !ketemu {

		fmt.Println("Data tidak ditemukan")
	}
}
func sequentialSearchRuangan(A tabTask, n int) {

	var cari string
	var i int
	var ketemu bool

	fmt.Print("Cari ruangan : ")
	fmt.Scan(&cari)

	ketemu = false

	for i = 0; i < n; i++ {

		if A[i].Ruangan == cari {

			fmt.Println("\nData ditemukan")
			fmt.Println(A[i])

			ketemu = true
		}
	}

	if !ketemu {

		fmt.Println("Data tidak ditemukan")
	}
}
func selectionSortKesulitan(A *tabTask, n int, asc bool) {

	var i, j, idx int
	var temp Task

	for i = 0; i < n-1; i++ {
		// menyimpan nilai minimun sementara
		idx = i
		// mencari lg nilai yg lebih kecil dari si idx = i 
		for j = i + 1; j < n; j++ {

			if asc {

				if (*A)[j].Kesulitan < (*A)[idx].Kesulitan {
					idx = j
				}

			} else {

				if (*A)[j].Kesulitan > (*A)[idx].Kesulitan {
					idx = j
				}
			}
		}

		temp = (*A)[i]
		(*A)[i] = (*A)[idx]
		(*A)[idx] = temp
	}

	fmt.Println("Data berhasil diurutkan")
}
func selectionSortDurasi(A *tabTask, n int, asc bool) {

	var i, j, idx int
	var temp Task

	for i = 0; i < n-1; i++ {

		idx = i

		for j = i + 1; j < n; j++ {

			if asc {

				if (*A)[j].Durasi < (*A)[idx].Durasi {
					idx = j
				}

			} else {

				if (*A)[j].Durasi > (*A)[idx].Durasi {
					idx = j
				}
			}
		}

		temp = (*A)[i]
		(*A)[i] = (*A)[idx]
		(*A)[idx] = temp
	}

	fmt.Println("Data berhasil diurutkan")
}
func insertionSortDurasi(A *tabTask, n int, asc bool) {

	var i, j int
	var temp Task

	for i = 1; i < n; i++ {

		temp = (*A)[i]
		j = i - 1

		if asc {

			for j >= 0 && (*A)[j].Durasi > temp.Durasi {

				(*A)[j+1] = (*A)[j]
				j--
			}

		} else {

			for j >= 0 && (*A)[j].Durasi < temp.Durasi {

				(*A)[j+1] = (*A)[j]
				j--
			}
		}

		(*A)[j+1] = temp
	}

	fmt.Println("Data berhasil diurutkan")
}
func insertionSortKesulitan(A *tabTask, n int, asc bool) {

	var i, j int
	var temp Task

	for i = 1; i < n; i++ {

		temp = (*A)[i]
		j = i - 1 //selalu dipindahkan ke kiri

		if asc {
			// geser semua nilai besar
			for j >= 0 && (*A)[j].Kesulitan > temp.Kesulitan {

				(*A)[j+1] = (*A)[j]
				j = j - 1
			}

		} else {
			// geser semua nilai kecil
			for j >= 0 && (*A)[j].Kesulitan < temp.Kesulitan {

				(*A)[j+1] = (*A)[j]
				j = j - 1
			}
		}

		(*A)[j+1] = temp
	}

	fmt.Println("Data berhasil diurutkan")
}
func binarySearchRuangan(A *tabTask, n int) {
	
	var kiri, kanan, tengah int
	var cari string
	var i, j int
	var temp Task
	var ketemu bool 
	
	for i = 0; i < n-1; i++ {
		
		for j = 0; j < n-i-1; j++ {
			//ascending
			if (*A)[j].Ruangan > (*A)[j+1].Ruangan {

				temp = (*A)[j]
				(*A)[j] = (*A)[j+1]
				(*A)[j+1] = temp
			}
		}
	}
	fmt.Print("Cari ruangan : ")
	fmt.Scan(&cari)
	kiri = 0
	kanan = n - 1
	ketemu = false
	for kiri <= kanan && !ketemu {

		tengah = (kiri + kanan) / 2

		if (*A)[tengah].Ruangan == cari {

			ketemu = true 
			
		} else if cari < (*A)[tengah].Ruangan {

			kanan = tengah - 1

		} else {

			kiri = tengah + 1
		}
	}
	if ketemu {
		
		fmt.Println("Data ditemukan")
		fmt.Println((*A)[tengah])
		
	} else {
		
		fmt.Println("Data tidak ditemukan")
		
	}
}
func binarySearchNama(A *tabTask, n int) {

	var kiri, kanan, tengah int
	var cari string
	var i, j int
	var temp Task
	var ketemu bool
	// ini 2 untuk mengurutkan data karena binary harus terurut
	for i = 0; i < n-1; i++ {

		for j = 0; j < n-i-1; j++ {

			if (*A)[j].Nama > (*A)[j+1].Nama {

				temp = (*A)[j]
				(*A)[j] = (*A)[j+1]
				(*A)[j+1] = temp
			}
		}
	}

	fmt.Print("Cari nama tugas : ")
	fmt.Scan(&cari)

	kiri = 0
	kanan = n - 1
	ketemu = false

	for kiri <= kanan && !ketemu {

		tengah = (kiri + kanan) / 2

		if (*A)[tengah].Nama == cari {

			ketemu = true

		} else if cari < (*A)[tengah].Nama {

			kanan = tengah - 1

		} else {

			kiri = tengah + 1
		}
	}
	if ketemu {
		
		fmt.Println("Data ditemukan")
		fmt.Println((*A)[tengah])
		
	} else {

	fmt.Println("Data tidak ditemukan")
	
	}
}
func tampilkanStatistik(A tabTask, n int) {

	var i int
	var jumlahSelesai int
	var totalDurasi int
	var rataRata float64

	jumlahSelesai = 0
	totalDurasi = 0

	for i = 0; i < n; i++ {

		if A[i].SudahSelesai {
			jumlahSelesai = jumlahSelesai + 1
		}

		totalDurasi = totalDurasi + A[i].Durasi
	}

	if n > 0 {
		rataRata = float64(totalDurasi) / float64(n)
	}

	fmt.Println("\n=== STATISTIK TUGAS ===")
	fmt.Println("Jumlah tugas selesai :", jumlahSelesai)
	fmt.Println("Jumlah seluruh tugas :", n)
	fmt.Printf("Rata-rata durasi     : %.2f menit\n", rataRata)
}
func main() {

	var daftarTugas tabTask
	var n int

	var menu int
	var pilih int
	var urut int
	var selesai bool

	selesai = false

	inisialisasiData(&daftarTugas, &n)

	for !selesai{

		fmt.Println("\n===== TASKMATE =====")
		fmt.Println("1. Tambah Tugas")
		fmt.Println("2. Tampilkan Tugas")
		fmt.Println("3. Cari Tugas")
		fmt.Println("4. Urutkan Tugas")
		fmt.Println("5. Ubah Tugas")
		fmt.Println("6. Hapus Tugas")
		fmt.Println("7. Statistik Tugas")
		fmt.Println("0. Keluar")

		fmt.Print("Pilih menu : ")
		fmt.Scan(&menu)

		if menu == 1 {

			tambahTugas(&daftarTugas, &n)

		} else if menu == 2 {

			tampilkanTugas(daftarTugas, n)

		} else if menu == 3 {

			fmt.Println("\n=== MENU SEARCH ===")
			fmt.Println("1. Sequential Search Nama")
			fmt.Println("2. Sequential Search Ruangan")
			fmt.Println("3. Binary Search Ruangan")
			fmt.Println("4. Binary Search Nama")

			fmt.Print("Pilih : ")
			fmt.Scan(&pilih)

			if pilih == 1 {

				sequentialSearchNama(daftarTugas, n)

			} else if pilih == 2 {

				sequentialSearchRuangan(daftarTugas, n)

			} else if pilih == 3 {

				binarySearchRuangan(&daftarTugas, n)
			
			}  else if pilih == 4 {

				binarySearchNama(&daftarTugas, n)
			}


		} else if menu == 4 {

			fmt.Println("\n=== MENU SORT ===")
			fmt.Println("1. Selection Sort Kesulitan")
			fmt.Println("2. Selection Sort Durasi")
			fmt.Println("3. Insertion Sort Durasi")
			fmt.Println("4. Insertion Sort Kesulitan")

			fmt.Print("Pilih : ")
			fmt.Scan(&pilih)

			fmt.Println("1. Ascending")
			fmt.Println("2. Descending")

			fmt.Print("Urutan : ")
			fmt.Scan(&urut)

			if pilih == 1 {

				if urut == 1 {

					selectionSortKesulitan(&daftarTugas, n, true)

				} else {

					selectionSortKesulitan(&daftarTugas, n, false)
				}

			} else if pilih == 2 {

				if urut == 1 {

					selectionSortDurasi(&daftarTugas, n, true)

				} else {

					selectionSortDurasi(&daftarTugas, n, false)
				}
				
			} else if pilih == 3 {
				
				if urut == 1 {
					
					insertionSortDurasi(&daftarTugas, n, true)
					
				} else {
					
					insertionSortDurasi(&daftarTugas, n, false)
					
				}
			} else if pilih == 4 {
				
				if urut == 1 {
					
					insertionSortKesulitan(&daftarTugas, n, true)
					
				} else {
					insertionSortKesulitan(&daftarTugas, n, false)
				}
			}

		} else if menu == 5 {

			ubahTugas(&daftarTugas, n)

		} else if menu == 6 {

			hapusTugas(&daftarTugas, &n)
			
		} else if menu == 7 {
			
			tampilkanStatistik(daftarTugas, n)
			
		} else if menu == 0 {

			fmt.Println("TerimaKasih telah menggunakan TaskMate!")
			selesai = true

		} else {

			fmt.Println("Menu tidak tersedia")
		}
	}
}
