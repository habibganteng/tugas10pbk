<template>
  <div class="daftar-buku">
    <h3>Daftar Buku Fiksi</h3>
    <div class="search-box">
      <input 
        type="text" 
        v-model="searchQuery" 
        placeholder="Cari buku..."
        @input="filterBuku"
      >
    </div>
    <div class="buku-grid">
      <div class="buku-card" v-for="buku in filteredBuku" :key="buku.id">
        <div class="cover">
          <img :src="buku.gambar" :alt="buku.judul">
        </div>
        <div class="info">
          <h4>{{ buku.judul }}</h4>
          <p class="penulis">{{ buku.pengarang }}</p>
          <p class="genre">{{ buku.genre }}</p>
          <p class="sinopsis">{{ buku.sinopsis }}</p>
          <div class="rating">
            <span v-for="i in 5" :key="i">★</span>
            <span>({{ buku.rating }})</span>
          </div>
          <button @click="pinjamBuku(buku.id)">Pinjam</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DaftarBuku',
  data() {
    return {
      searchQuery: '',
      daftarBuku: [
        {
          id: 1,
          judul: 'Laskar Pelangi',
          pengarang: 'Andrea Hirata',
          genre: 'Novel',
          sinopsis: 'Kisah persahabatan 10 anak di Belitung yang penuh lika-liku kehidupan.',
          rating: 4.7,
          gambar: '/img/buku/laskar-pelangi.jpg',
          tersedia: true
        },
        {
          id: 2,
          judul: 'Dilan 1990',
          pengarang: 'Pidi Baiq',
          genre: 'Novel Romantis',
          sinopsis: 'Kisah cinta masa SMA antara Dilan dan Milea di Bandung tahun 1990.',
          rating: 4.5,
          gambar: '/img/buku/dilan-1990.jpg',
          tersedia: true
        },
        {
          id: 3,
          judul: 'Naruto Vol. 1',
          pengarang: 'Masashi Kishimoto',
          genre: 'Komik Shonen',
          sinopsis: 'Petualangan Naruto Uzumaki, ninja muda yang bercita-cita menjadi Hokage.',
          rating: 4.8,
          gambar: 'img/buku/naruto.jpg',
          tersedia: true
        },
        {
          id: 4,
          judul: 'Bumi Manusia',
          pengarang: 'Pramoedya Ananta Toer',
          genre: 'Novel Sejarah',
          sinopsis: 'Kisah Minke, pemuda Jawa di era kolonial yang mencari jati diri.',
          rating: 4.9,
          gambar: 'img/buku/bumi-manusia.jpg',
          tersedia: false
        },
        {
          id: 5,
          judul: 'One Piece Vol. 1',
          pengarang: 'Eiichiro Oda',
          genre: 'Komik Petualangan',
          sinopsis: 'Petualangan Luffy dan kru Topi Jerami mencari harta karun legendaris.',
          rating: 4.9,
          gambar: 'img/buku/one-piece.jpg',
          tersedia: true
        },
        {
          id: 6,
          judul: 'Perahu Kertas',
          pengarang: 'Dee Lestari',
          genre: 'Novel Romantis',
          sinopsis: 'Kisah cinta rumit antara Keenan dan Kugy yang penuh lika-liku.',
          rating: 4.4,
          gambar: 'img/buku/perahu-kertas.jpg',
          tersedia: true
        },
        {
          id: 7,
          judul: 'Detektif Conan Vol. 1',
          pengarang: 'Gosho Aoyama',
          genre: 'Komik Detektif',
          sinopsis: 'Shinichi Kudo yang berubah menjadi anak kecil dan memecahkan berbagai kasus.',
          rating: 4.6,
          gambar: 'img/buku/detektif-conan.jpg',
          tersedia: true
        },
        {
          id: 8,
          judul: 'Ronggeng Dukuh Paruk',
          pengarang: 'Ahmad Tohari',
          genre: 'Novel',
          sinopsis: 'Kisah tragis seorang penari ronggeng di pedesaan Jawa tahun 1960-an.',
          rating: 4.5,
          gambar: 'img/buku/ronggeng-dukuh-paruk.jpg',
          tersedia: true
        }
      ],
      filteredBuku: []
    }
  },
  created() {
    this.filteredBuku = [...this.daftarBuku]
  },
  methods: {
    filterBuku() {
      this.filteredBuku = this.daftarBuku.filter(buku => {
        return (
          buku.judul.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          buku.pengarang.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          buku.genre.toLowerCase().includes(this.searchQuery.toLowerCase())
        )
      })
    },
    pinjamBuku(id) {
      const buku = this.daftarBuku.find(b => b.id === id)
      if (buku.tersedia) {
        alert(`Anda telah meminjam buku: ${buku.judul}`)
      } else {
        alert('Maaf, buku sedang tidak tersedia')
      }
    }
  }
}
</script>

<style scoped>
.daftar-buku {
  padding: 1rem;
}
.search-box {
  margin-bottom: 1rem;
}
.search-box input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}
.buku-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1rem;
}
.buku-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  display: flex;
  transition: transform 0.3s;
}
.buku-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}
.cover {
  width: 120px;
  background: #f5f5f5;
}
.cover img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.info {
  padding: 1rem;
  flex: 1;
}
.info h4 {
  margin: 0 0 0.5rem 0;
  color: #333;
}
.penulis {
  font-size: 0.9rem;
  color: #666;
  margin: 0 0 0.5rem 0;
}
.genre {
  display: inline-block;
  background: #f0f0f0;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  font-size: 0.8rem;
  margin: 0 0 0.5rem 0;
}
.sinopsis {
  font-size: 0.9rem;
  color: #555;
  margin: 0 0 0.5rem 0;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.rating {
  color: gold;
  margin-bottom: 0.5rem;
}
.rating span:last-child {
  color: #666;
  margin-left: 0.5rem;
}
button {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}
button:hover {
  background-color: #3aa876;
}
</style>