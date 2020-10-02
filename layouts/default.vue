<template>
  <div>
    <div class="position-relative">
      <div class="position-absolute w-100 font-weight-bold px-5 mt-3 text-white nav-controls" style="z-index: 999;">
        <span class="text-white"><img src="/logo.svg" style="width: 35px; height: 35px;" class="mr-3" alt=""></span>
        <span class="fake-link text-white float-right" style="margin-top: 3px;" @click="nextQuote()">NEXT QUOTE</span>
      </div>
      <div class="position-absolute d-flex align-items-center w-100 min-vh-100">
        
          <div class="w-100 mb-2">
            <transition name="t-fade" appear>
              <div class="quote-block mt-5 mx-5 mb-3 pt-5 pb-5 px-5 text-white rounded" v-show="showQuote">
                <div>
                  <h1 class="quote-text text-center">
                    “{{ currQuote }}”
                  </h1>
                </div>
                <div class="py-1 w-50 mx-auto">
                  <hr>
                </div>
                <div class="mt-1">
                  <div class="d-flex w-100 justify-content-center">
                    <div class="p-2 bd-highlight">
                      <img :src="currAvatar === '' ? '/avatar_02.png' : currAvatar" alt="" class="mr-2" style="width: 70px; height: 70px;">
                    </div>
                    <div class="p-2 bd-highlight">
                      <span class="author-text text-left text-uppercase font-weight-bold">
                        {{ currAuthor }}
                      </span><br>
                      <span class="author-sub-text text-left font-weight-light font-italic">
                        {{ currAuthorSub }}
                      </span>
                    </div>
                  </div>
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
      currAvatar: '',
      showQuote: true,
      queueIsOpen: true,
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
          authorSub: 'The “Oracle of Omaha”',
          img: '/avatars/warren-buffet.png'
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
        },
        {
          quote: 'Be fearful when others are greedy, and greedy when others are fearful.',
          author: 'Warren Buffet',
          authorSub: 'The “Oracle of Omaha”',
          img: '/avatars/warren-buffet.png'
        },
        {
          quote: 'You can be free. You can live and work anywhere in the world. You can be independent from routine and not answer to anybody.',
          author: 'Alexander Elder',
          authorSub: 'Professor, Columbia University'
        },
        {
          quote: 'I believe in analysis and not forecasting.',
          author: 'Nicolas Darvas',
          authorSub: 'Dancer; Self-taught Trader'
        },
        {
          quote: 'A lot of people get so enmeshed in the markets that they lose their perspective. Working longer does not necessarily equate with working smarter. In fact, sometimes is the other way around.',
          author: 'Martin Schwartz',
          authorSub: 'U.S Investing Champion, 1984'
        },
        {
          quote: 'The secret to being successful from a trading perspective is to have an indefatigable and an undying and unquenchable thirst for information and knowledge.',
          author: 'Paul Tudor Jones',
          authorSub: 'Predicted the 1987 Black Monday Crash'
        },
        {
          quote: 'All the math you need in the stock market you get in the fourth grade.',
          author: 'Peter Lynch',
          authorSub: 'American Investor, Mutual Fund Manager, Philanthropist',
          img: '/avatars/peter-lynch.png'
        },
        {
          quote: 'My friends thought I was going to fail.',
          author: 'Cathie Wood',
          authorSub: 'CEO, ARK Investment Management',
          img: '/avatars/cathie-wood.png'
        },
        {
          quote: 'I was an investor doing well and decided to be an entrepreneur.',
          author: 'Lynn Jurich',
          authorSub: 'CEO, Sunrun',
          img: '/avatars/lynn-jurich.png'
        },
        {
          quote: 'The ancient Egyptians were amazing, but if aliens built the pyramids, they would\'ve left behind a computer or something',
          author: 'Elon Musk on Twitter',
          authorSub: 'CEO, Tesla & Space X',
          img: '/avatars/elon-musk.png'
        },
        {
          quote: 'Try to figure out what your skill set is and apply that to the markets. If you are really good at accounting, you might be good as a value investor. If you are strong in computers and math, you might do best with a quantitative approach.” “If you aren’t going to be a professional investor, just index.',
          author: 'Edward O. Thorp',
          authorSub: 'Legendary Options Trader',
          img: '/avatars/edward-o-thorp.png'
        },
      ]
    }
  },
  methods: {
    nextQuote: function () {
      this.currIndex++

      // if (this.currIndex >= this.quotes.length) {
      //   this.currIndex = 0
      // }
      this.queueIsOpen = false

      this.currIndex = Math.floor(Math.random() * this.quotes.length); 

      this.showQuote = false

      let self = this

      if (!self.queueIsOpen) {
        setTimeout(function () {        
          if (self.quotes[self.currIndex].img) {
            self.currAvatar = self.quotes[self.currIndex].img
          } else {
            self.currAvatar = ''
          }

          self.currQuote = self.quotes[self.currIndex].quote
          self.currAuthor = self.quotes[self.currIndex].author
          self.currAuthorSub = self.quotes[self.currIndex].authorSub

          self.showQuote = true
          self.queueIsOpen = true
        }, 600)
      }
    }
  },
  mounted() {
    this.currQuote = this.quotes[this.currIndex].quote
    this.currAuthor = this.quotes[this.currIndex].author
    this.currAuthorSub = this.quotes[this.currIndex].authorSub

    let self = this
    setInterval(() =>  self.nextQuote(), 10000)
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
  background: url(/unsplash_02.jpg) no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.t-fade-enter-active, .t-fade-leave-active {
  transition: opacity .8s;
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
