<script>
    import {getContext} from 'svelte';

    let name2 = getContext("name2");
</script>
<p>Nested component: {name2}</p>