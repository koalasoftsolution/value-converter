<template>
    <div>
        <Header></Header>
        <Body></Body>
        <Footer></Footer>
    </div>
</template>

<script>
import Header from '../header/header'
import Body from '../body/body'
import Footer from '../footer/footer'
export default {
  name: 'layout',
  components: {
    Header,
    Body,
    Footer,
  }
}
</script>

