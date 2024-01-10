<template>
  <div>
    <h2 class="text-center">Isi Buku Tamu</h2>
    <br />
    <div v-if="sukses" class="alert alert-success">Berhasil Tersimpan</div>
    <form @submit.prevent="simpan()">
      <div class="mb-3">
        <input v-model="form.nama" type="text" placeholder="Nama" class="form-control" />
      </div>
      <div class="mb-3">
        <select v-model="form.anggota" class="form-control">
          <option value="pilih keanggotaan">Pilih keanggotaan</option>
          <option value="1">Siswa</option>
          <option value="2">Guru</option>
          <option value="3">Staf</option>
        </select>
      </div>
      <div v-if="form.anggota == 1" class="mb-3">
        <input v-model="form.kelas" type="text" class="form-control" placeholder="kelas" />
      </div>
      <div class="mb-3">
        <textarea v-model="form.keperluan" cols="30" rows="3" placeholder="keperluan" class="form-control"></textarea>
      </div>
      <button type="submit" class="btn btn-outline-primary">Kirim</button>
      <nuxt-link to="/">Kembali</nuxt-link>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const form = reactive({
  nama: "",
  anggota: "",
  kelas: "",
  keperluan: "",
});

const sukses = ref(false);

async function simpan() {
  sukses.value = false;
  const { error } = await supabase.from("pengunjung").insert(form);

  if (!error) {
    sukses.value = true;
    form.nama = ''
    form.anggota = ''
    form.kelas = ''
    form.keperluan = ''
  }
}
</script>
