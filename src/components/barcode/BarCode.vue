<template>
  <div>
    <canvas
      :style="{height: height, width: width}"
      :height="height"
      :width="width" ref="canvas"></canvas>
  </div>
</template>

<script>
  import barcode from './barcode'


  export default {
    props: {
      value: String,
      height: {
        type: String,
        default: 10
      },
      width: {
        type: String,
        default: 10
      },

      bgColor: {
        type: String,
        default: '#999999'
      },
      fgColor: {
        type: String,
        default: '#000000'
      }

    },
    mounted () {
      this.$nextTick(() => {
        this.render()
      })
    },
    data () {
      return {
        imgData: ''
      }
    },
    watch: {
      value () {
        this.render()
      },
      size () {
        this.render()
      },
      level () {
        this.render()
      },
      bgColor () {
        this.render()
      },
      fgColor () {
        this.render()
      }
    },
    methods: {
      render () {


        const canvas = this.$refs.canvas

        const ctx = canvas.getContext('2d')


//        ctx.scale(0.5, 1)
        ctx.fillStyle = this.bgColor
        ctx.fillRect(0, 0, canvas.width ,  canvas.height)
        ctx.fillStyle = this.fgColor
//        ctx.fillRect(1, 1,  3 ,  3)
//        this.value = "19819461086501025812"
        //    console.log("this.value "+this.value )

        var codedStr = barcode.code128(this.value)

        var s = codedStr;
        //     console.log("codedStr="+codedStr);
        //   console.log("codedStr="+codedStr.length);
        var width = canvas.width;
        var minScale = 1;
        var length = 0;
        for ( var pos = 0; pos < s.length; pos += 2 )
        {
          var w = parseInt( s.charAt( pos ) )
          var w2 = parseInt( s.charAt( pos + 1 ) )
          length = length + minScale * w + minScale * w2;
        }
        var calcScale = parseInt( width / length );
        let offset = 0 + (width - calcScale * length) / 2;
//        offset=0;
        //   console.log( "cavW=" + width )
        //    console.log( "length=" + length )
        //    console.log( "offset=" + offset )
        //    console.log( "calcScale=" + calcScale )



        for ( var pos = 0; pos < s.length; pos += 2 )
        {
          var w = parseInt( s.charAt( pos ) )
          var w2 = parseInt( s.charAt( pos + 1 ) )
          ctx.fillRect( offset, 0, calcScale * w, canvas.height )
          offset = offset + calcScale * w + calcScale * w2;
        }



      }
    }
  }


</script>
