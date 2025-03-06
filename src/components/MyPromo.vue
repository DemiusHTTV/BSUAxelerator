<template>
    <section class="" style="
						background-image: url('');
						background-position: top;
						background-repeat: no-repeat;
						background-size: cover;
					">
        <div class="py-5 container">
            <div class="py-5-middle-container">
                <h3 class="h3">Номер аукциона</h3>
                <p><input class="search" placeholder="Поиск интересующего аукциона"></p>
                <button class="btn btn-success btn-md mt-5">Найти</button>
                <p class="pt-5 fw-medium">
                    <slot></slot>                    
                </p>
            </div>
        </div>
    </section>
</template>
<script>
export default{
    name:'MyPromo'
}
</script>