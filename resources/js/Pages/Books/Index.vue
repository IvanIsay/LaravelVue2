<script setup>

    import BreezeAuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
    import { Head } from "@inertiajs/inertia-vue3";
    import BreezeButton from "@/Components/PrimaryButton.vue";
    import { Link } from "@inertiajs/inertia-vue3";
    import { Inertia } from "@inertiajs/inertia";
    import { useForm } from '@inertiajs/inertia-vue3'

    const props = defineProps({
        books: {
            type: Object,
            default: () => ({}),
        },
    });
    const form = useForm();

    function destroy(id) {
        if (confirm("¿ Seguro que quieres Borrarlo ?")) {
            form.delete(route('books.destroy', id));
        }
    }

</script>

    <template>

      <Head title="Libros" />

    <BreezeAuthenticatedLayout>

            <template #header>
                <h2 class="text-xl font-semibold leading-tight text-gray-800">
                    Listado de Libros
                </h2>
            </template>

            <div class="py-12">

                <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                   

                    <!-- <div
                        v-if="$page.props.flash.message"
                        class="p-4 mb-4 text-sm text-green-700 bg-green-100 rounded-lg dark:bg-green-200 dark:text-green-800"
                        role="alert"
                    >
                        <span class="font-medium">
                            {{ $page.props.flash.message }}
                        </span>
                    </div> -->


                    <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                        <div class="p-6 bg-white border-b border-gray-200">
                           
                            <div class="mb-4 mt-4">
                                <Link :href="route('books.create')">
                                    <BreezeButton> Agregar Libro </BreezeButton>
                                </Link>
                            </div>

                             <div class="relative overflow-x-auto shadow-md sm:rounded-lg" >

                                <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400" >

                                    <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                                        <tr>
                                            <th scope="col" class="px-6 py-3">Id:</th>
                                            <th scope="col" class="px-6 py-3"> Titulo: </th>
                                            <th scope="col" class="px-6 py-3"> Autor: </th>
                                            <th scope="col" class="px-6 py-3"> Editar: </th>
                                            <th scope="col" class="px-6 py-3"> Borrar: </th>
                                        </tr>
                                    </thead>

                                    <tbody>
                                        <tr v-for="book in books" :key="book.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" >
                                            
                                            <th scope="row"  class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                                                {{ book.id }}
                                            </th>

                                            <th scope="row" class="px-6 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                                                {{ book.title }}
                                            </th>

                                            <td class="px-6 py-4">
                                                {{ book.autor }}
                                            </td>

                                            <td class="px-6 py-4">
                                                <Link :href=" route( 'books.edit', book.id )"
                                                class="px-4 py-2 text-white bg-blue-600 rounded-lg" > Editar
                                            </Link>
                                            </td>

                                            <td class="px-6 py-4">
                                                <BreezeButton class="bg-red-700" @click="destroy(book.id)">
                                                    Borrar
                                                </BreezeButton>
                                            </td>

                                        </tr>

                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>


        </BreezeAuthenticatedLayout>
    </template>