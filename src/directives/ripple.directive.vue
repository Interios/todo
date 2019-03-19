<script>
export default {
    inserted: function (el) {
        // Переключаем фокус на элемент
        el.addEventListener('click', function(e) {
            var rect = el.getBoundingClientRect(),
                px   = 'px',
                ripple = document.createElement("span");

                ripple.setAttribute("class", "ripple");
                ripple.style.left = e.clientX - rect.left + px;
                ripple.style.top = e.clientY - rect.top + px;
                el.appendChild(ripple);

            setTimeout(() => {
                el.removeChild(ripple);
            }, 500);
        })
    }
}
</script>

<style>
    .ripple {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background: red;
        display: inline-block;
        transform: scale(0) translate(-50%, -50%);
        position: absolute;
        opacity: 1;
        animation: ripple .5s linear;
        transform-origin: left top;
    }

    @keyframes ripple {
        100% {
            transform: scale(2.5) translate(-50%, -50%);
            opacity: 0;
        }
    }
</style>