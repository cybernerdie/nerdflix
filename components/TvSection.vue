<template>
 <div class="content__head">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <!-- content title -->

              <h2 class="content__title" style="color: #ffd80e">
                {{ title }}
              </h2>
              <!-- end content title -->
            </div>
          </div>
        </div>
      </div>
</template>

<script>
export default {
   name: 'TvSection',
    props: ['title'],
}
</script>
