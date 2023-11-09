<template>
  <div class="">
    <OpenDialog
      :openDialog="modalTest"
      @closeDialog="modalTest = false"
    ></OpenDialog>
    <div class="">
      <p>Welcome</p>

      <Button prepend-icon variant="plain">
        <template #icon> icon </template>Button
      </Button>
    </div>

    <div class="max-w-6xl grid grid-cols-2 mx-auto gap-6">
      <Cards showTitle showSubTitle loading rounded variant="outline">
        <template #title>Hereisthe </template>
        <template #subtitle>here is subtitle</template>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Ut, distinctio
        quam enim aliquid necessitatibus amet reiciendis voluptas beatae est,
        pariatur, vel aut aspernatur minus sint totam temporibus dolorum atque
        voluptate?
        <template #action>
          <button>ClickMe</button>
        </template>
      </Cards>

      <Cards showTitle showSubTitle variant="outline">
        <template #title>Another Card </template>
        <template #subtitle>here is subtitle</template>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Ut, distinctio
        quam enim aliquid necessitatibus amet reiciendis voluptas beatae est,
        pariatur, vel aut aspernatur minus sint totam temporibus dolorum atque
        voluptate?
        <template #action>
          <button>ClickMe</button>
        </template>
      </Cards>
    </div>
    <Chip prependIcon apendIcon variant="elevated"
      >chipr
      <template #icon> icon</template>
    </Chip>

    <button
      @click="modalTest = true"
      class="px-4 py-2 bg-gray-400 text-white relative"
    >
      Open Dialog
    </button>
  </div>
</template>

<script setup>
const modalTest = ref(false);
</script>
