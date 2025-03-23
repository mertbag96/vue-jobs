 <script setup>
import Logo from './Logo.vue'
import Menu from './Menu.vue'
</script>

 <template>
    <nav class="bg-green-700 border-b border-green-500">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="flex h-20 items-center justify-between">
          <div class="flex flex-1 items-center justify-center md:items-stretch md:justify-start">
            <!-- Logo -->
            <Logo />

            <!-- Menu -->
            <Menu />
          </div>
        </div>
      </div>
    </nav>
 </template>