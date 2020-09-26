<template>
  <div>
    <div class="position-relative">

      <div class="position-absolute w-100 text-right font-weight-bold pr-5 mt-3 text-white nav-controls" style="z-index: 999;">
        <span class="fake-link text-white" @click="nextQuote()">NEXT QUOTE</span>
      </div>
      <div class="position-absolute d-flex align-items-center text-center w-100 min-vh-100">
        
          <div class="w-100 mb-2">
            <transition name="t-fade" appear>
              <div class="quote-block mt-5 mx-5 mb-3 pt-5 pb-4 px-5 text-white rounded" v-show="showQuote">
                <div>
                  <h1 class="quote-text">
                    "{{ currQuote }}"
                  </h1>
                </div>
                <div class="py-1 w-50 mx-auto">
                  <hr>
                </div>
                <div class="mt-1">
                  <span class="author-text text-uppercase font-weight-bold">
                    {{ currAuthor }}
                  </span><br>
                  <span class="author-sub-text font-weight-light font-italic">
                    {{ currAuthorSub }}
                  </span>
                </div>
              </div>
            </transition>
          </div>
      </div>
      <!-- <div class="full-page-bg min-vh-100">
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currQuote: '',
      currAuthor: '',
      currAuthorSub: '',
      showQuote: true,
      currIndex: 0,
      quotes: [
        {
          quote: 'Every trader has strengths and weakness. Some are good holders of winners, but may hold their losers a little too long. Others may cut their winners a little short, but are quick to take their losses. As long as you stick to your own style, you get the good and bad in your own approach.',
          author: 'Michael Marcus',
          authorSub: 'Commodities Trader'
        },
        {
          quote: 'Markets can remain irrational longer than you can remain solvent.',
          author: 'John Maynard Keynes',
          authorSub: 'British Economist, Founder of Keynesian Economics'
        },
        {
          quote: 'You don\'t need to be a rocket scientist. Investing is not a game where the guy with the 160 IQ beats the guy with 130 IQ.',
          author: 'Warren Buffet',
          authorSub: 'The “Oracle of Omaha”'
        },
        {
          quote: 'Markets are constantly in a state of uncertainty and flux and money is made by discounting the obvious and betting on the unexpected.',
          author: 'George Soros',
          authorSub: 'Philanthropist; also "The Man Who Broke the Bank of England"'
        },
        {
          quote: 'The key to trading success is emotional discipline. If intelligence were the key, there would be a lot more people making money trading… I know this will sound like a cliche, but the single most important reason that people lose money in the financial markets is that they don’t cut their losses short.',
          author: 'Victor Sperandeo',
          authorSub: 'US-based Trader; also "Trader Vic"'
        }
      ]
    }
  },
  methods: {
    nextQuote: function () {
      this.currIndex++

      if (this.currIndex >= this.quotes.length) {
        this.currIndex = 0
      }

      this.showQuote = false

      let self = this

      setTimeout(function () {
        self.currQuote = self.quotes[self.currIndex].quote
        self.currAuthor = self.quotes[self.currIndex].author
        self.currAuthorSub = self.quotes[self.currIndex].authorSub

        self.showQuote = true
      }, 600)
    }
  },
  mounted() {
    this.currQuote = this.quotes[this.currIndex].quote
    this.currAuthor = this.quotes[this.currIndex].author
    this.currAuthorSub = this.quotes[this.currIndex].authorSub
  },
}
</script>

<style>
hr {
  border-top: 2px solid rgba(0,0,0,.1);
  border-color: white;
}

.quote-block {
  background-color: rgba(0,0,0, .56);
}

.quote-text {
  /* font-size: 3.5vw; */

  font-size: 36px;
  font-family: Georgia;
}

.author-text {
  font-family: 'Helvetica', 'Helvetica Neue';
  /* font-size: 1.5vw; */
  font-size: 22px;
  letter-spacing: 2px;
}

.author-sub-text {
  /* font-size: 1.2vw; */
  font-size: 18px;
}

.rounded {
  border-radius: 10px!important;
}

.nav-controls {
  -webkit-font-smoothing: antialiased;
  -moz-font-smoothing: antialiased;
  letter-spacing: 1px;
  font-size: 1.1em; 
  font-family: arial;
}

html { 
  background: url(/unsplash_01.jpg) no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.t-fade-enter-active, .t-fade-leave-active {
  transition: opacity .4s;
}
.t-fade-enter, .t-fade-leave-active {
  opacity: 0;
}

.fake-link:hover {
  cursor: pointer;
  padding-bottom: 2px;
  border-bottom: 2px solid white;
}
</style>
