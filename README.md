# APlikasi-Notes

Penjelasan setiap logika java script

const notesContainer = document.querySelector('.notes-container');
const createBtn = document.querySelector('.btn');
let notes = document.querySelectorAll('.input-box');

function showNotes (){
    notesContainer.innerHTML = localStorage.getItem('notes');
}

showNotes();

function updateStorage(){
    localStorage.setItem('notes', notesContainer.innerHTML);
}



createBtn.addEventListener('click', () => {
    let inputBox = document.createElement('p');
    let img = document.createElement('img');
    inputBox.className = 'input-box';
    inputBox.setAttribute('contenteditable', 'true');
    img.src = 'images/delete.png';
    notesContainer.appendChild(inputBox).appendChild(img);
} )



notesContainer.addEventListener('click', function(e){
    if(e.target.tagName === 'IMG'){
        e.target.parentElement.remove();
        updateStorage();
    }

    else if(e.target.tagName === 'P'){
        notes = document.querySelectorAll('.input-box');
        notes.forEach(nt => {
            nt.onkeyup = function (){
                
                updateStorage();
            }
        })
    }
})


document.addEventListener('keydown', event => {
    if(event.key === 'Enter'){
        document.execCommand('insertLineBreak');
        event.preventDefault();

    }
})



Script JavaScript ini bertujuan untuk mengelola catatan yang dapat diedit dan disimpan dalam penyimpanan lokal browser. Berikut adalah logika dari script tersebut:

1. **Seleksi DOM**: 
   - [notesContainer] adalah elemen yang akan menampung semua catatan.
   - [createBtn]adalah tombol yang digunakan untuk membuat catatan baru.
   - [notes] adalah NodeList dari semua elemen dengan kelas `.input-box` yang mewakili setiap catatan.

2. **Menampilkan Catatan**:
   - Fungsi [showNotes()]mengambil data dari [localStorage]dengan kunci 'notes' dan menetapkannya sebagai konten HTML dari [notesContainer]. Fungsi ini dipanggil saat script dimuat untuk menampilkan catatan yang telah disimpan sebelumnya.

3. **Menyimpan Perubahan**:
   - Fungsi [updateStorage()] menyimpan konten HTML dari [notesContainer] ke [localStorage] dengan kunci 'notes'. Ini memastikan bahwa semua perubahan pada catatan disimpan secara persisten.

4. **Membuat Catatan Baru**:
   - Event listener pada [createBtn] menangani pembuatan catatan baru. Saat tombol diklik, elemen `<p>` (inputBox) dan `<img>` (untuk tombol hapus) dibuat. [inputBox] diatur sebagai editable dan [img] diatur sebagai ikon hapus. Kemudian, [inputBox] ditambahkan ke [notesContainer] dan [img] ditambahkan ke [inputBox].

5. **Menghapus dan Mengedit Catatan**:
   - Event listener pada [notesContainer] menangani klik pada elemen di dalamnya. Jika elemen yang diklik adalah `<img>`, elemen induk (yang merupakan [inputBox]) dihapus dan penyimpanan diperbarui. Jika elemen yang diklik adalah `<p>`, NodeList [notes]diperbarui dan event [onkeyup] ditetapkan untuk setiap [inputBox] untuk memperbarui penyimpanan setiap kali ada perubahan.

6. **Menangani Enter Key**:
   - Event listener pada dokumen menangani tekanan tombol 'Enter'. Alih-alih membuat baris baru secara default, script ini memasukkan jeda baris ([insertLineBreak]) dan mencegah perilaku default. Ini memungkinkan pengguna untuk memasukkan baris baru dalam [inputBox]tanpa mengirim formulir atau membuat elemen baru.

Secara keseluruhan, script ini memungkinkan pengguna untuk membuat, mengedit, dan menghapus catatan teks yang disimpan secara lokal di browser, dengan antarmuka yang memungkinkan pengeditan langsung dan interaksi yang intuitif.