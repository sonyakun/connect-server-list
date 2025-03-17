<template>
    <div class="p-1 rounded-md">
        <span v-html="formattedText"></span>
    </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
    text: {
        type: String,
        required: true
    }
});

const formattedText = computed(() => {
    return convertToTailwind(props.text);
});

function convertToTailwind(text) {
    const formats = {
        '§0': 'color: #000000',
        '§1': 'color: #0000AA',
        '§2': 'color: #00AA00',
        '§3': 'color: #00AAAA',
        '§4': 'color: #AA0000',
        '§5': 'color: #AA00AA',
        '§6': 'color: #FFAA00',
        '§7': 'color: #C6C6C6',
        '§8': 'color: #555555',
        '§9': 'color: #5555FF',
        '§a': 'color: #55FF55',
        '§b': 'color: #55FFFF',
        '§c': 'color: #FF5555',
        '§d': 'color: #FF55FF',
        '§e': 'color: #FFFF55',
        '§f': 'color: #FFFFFF',
        '§g': 'color: #DDD605',
        '§h': 'color: #E3D4D1',
        '§i': 'color: #CECACA',
        '§j': 'color: #443A3B',
        '§m': 'color: #971607',
        '§n': 'color: #B4684D',
        '§p': 'color: #DEB12D',
        '§q': 'color: #119F36',
        '§s': 'color: #2CBAA8',
        '§t': 'color: #21497B',
        '§u': 'color: #9A5CC6',
        '§v': 'color: #EB7114',
        '§l': 'font-weight: bold',
        '§m': 'text-decoration: line-through',
        '§n': 'text-decoration: underline',
        '§o': 'font-style: italic',
        '§r': 'color: initial; font-weight: normal; text-decoration: none; font-style: normal',
    };

    return text.replace(/§[0-9a-flrmo]/g, match => {
        return `<span style="${formats[match] || ''};">`;
    }).replace(/(?=<\/span>)/g, '') + '</span>';
}
</script>