<template>
  <div>
    <button type="button" @click.prevent="increment(1)">按鈕</button>
    <pre>{{ state.count }}</pre>
    <hr />
    <button
      type="button"
      @click.prevent="addProduct({ title: 'A Book', price: Math.random() })"
    >
      按鈕
    </button>
    <pre>{{ storage.products }}</pre>
    <hr />
    <button type="button" @click.prevent="updateYearAndMonth('2022', 10)">
      按鈕
    </button>
    <pre>{{ year }}/{{ month }}</pre>
    <hr />
    <pre>{{ foo + 1 }}</pre>
    <hr />
    <p>Has published books:</p>
    <span>{{ publishedBooksMessage }}</span>
    <hr />
    <button type="button" @click.prevent="updateName('Ian Lan')">按鈕</button>
    <p>{{ fullName }}</p>
    <hr />
    <button type="button" @click.prevent="printTime">按鈕</button>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, computed } from 'vue';

// #1

const state = reactive({ count: 0 });

const increment = (num: number) => {
  state.count += num;
};

// #2

interface Product {
  title: string;
  price: number;
}

interface Storage {
  products: Product[];
}

const storage: Storage = reactive({ products: [] });

const addProduct = (product: Product) => {
  storage.products.push(product);
};

// #3

const year = ref<string | number>(2020);
const month = ref(1);

const updateYearAndMonth = (y: string | number, m: number) => {
  year.value = y;
  month.value = m;
};

// #4

const object = { foo: ref(1) };
const { foo } = object;

// #5

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery',
  ],
});

const publishedBooksMessage = computed(() => {
  return author.books.length ? 'Yes' : 'No';
});

// #6
const firstName = ref('John');
const lastName = ref('Doe');

const fullName = computed({
  get() {
    return `${firstName.value} ${lastName.value}`;
  },
  set(newValue: string) {
    [firstName.value, lastName.value] = newValue.split(' ');
  },
});

const updateName = (newFullName: string) => {
  fullName.value = newFullName;
};

// #7
const delay = (t: number) => new Promise((resolve) => setTimeout(resolve, t));

const printTime = async () => {
  console.log(Date.now());
  await delay(3000);
  console.log(Date.now());
};
</script>

<style></style>
