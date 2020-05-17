<template>
    <div class="card darken-1" :class="color">
        <div class="card-content white-text">
            <span class="card-title">
                <i class="fas" :class="icon"></i> {{ title }}
            </span>
            <span class="highlight-value">{{ value }}</span>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    title: String,
    value: String,
    icon: String,
    color: String,
  }    
}
</script>

<style scoped>

.card-title {
    font-size: 28px;
}

.highlight-value {
    font-size: 17px;
    margin-top: 14px;
    display: block;
}

.card-title {
    font-size: 28px;
}

</style>
