<template>
    <div id="container" style="width: 100%; height: 100vh"></div>
</template>

<script setup>
/* globals canvas */
import SvgCanvas from "../svgcanvas/svgcanvas.js";
import Editor from "../editor/Editor.js";
import { ref, onMounted /* nextTick */ } from "vue";

onMounted(() => {
    /* for available options see the file `docs/tutorials/ConfigOptions.md */
    const svgEditor = new Editor(document.getElementById("container"));
    svgEditor.init();
    svgEditor.setConfig({
        allowInitialUserOverride: true,
        extensions: [],
        noDefaultExtensions: false,
        userExtensions: [
            /* { pathName: './react-extensions/react-test/dist/react-test.js' } */
        ],
    });
    // Variable XDOMAIN below is created by Rollup for the Xdomain build (see rollup.config.js)
    /* globals XDOMAIN */
    try {
        // try clause to avoid js to complain if XDOMAIN undefined
        if (XDOMAIN) {
            svgEditor.setConfig({
                canvasName: "xdomain", // Namespace this
                allowedOrigins: ["*"],
            });
            console.info("xdomain config activated");
        }
    } catch (error) {
        /* empty fn */
    }
});
</script>
