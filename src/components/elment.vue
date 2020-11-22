<template>
    <div>
        <div class="form__item">
            <input list="animals" name="animal" id="animal">
            <datalist id="animals">
                <option value="Cat"></option>
                <option value="Dog"></option>
                <option value="Chicken"></option>
                <option value="Cow"></option>
                <option value="Pig"></option>
            </datalist>
        </div>
        <div class="form__item">
            <select id="animals2">
                <option value="Cat2">1</option>
                <option value="Dog2">2</option>
                <option value="Chicken2">3</option>
                <option value="Cow2">4</option>
                <option value="Pig2">5</option>
            </select>
        </div>
    </div>
</template>

<script>
    export default {
        name: "elment"
    }
</script>

<style scoped>

</style>