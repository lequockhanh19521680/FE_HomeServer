<script>
    import Footer from "./Footer/Footer.svelte";
	import Header from "./Header/Header.svelte";
    import HeaderNav from "./Header/HeaderNav.svelte";

	let text = "Portfolio của Khanh"
</script>
<HeaderNav />
<Header {text} />
<Footer />