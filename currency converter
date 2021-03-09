//index.html
<div class="main ui text container">
  
   <div class="ui dividing centered header"> 
     <h1>Currency Converter</h1>
     <h2>
       <i class="fa fa-dollar" style="color: #ffb3ba"></i>
       <i class="fa fa-gbp" style="color:#bae1ff"></i>
       <i class="fa fa-eur" style="color:#c6acc7"></i>
     </h2>
  </div>
  
   <div id="app"> </div> </div>

//style.css
body {
  background: #ADD8E6;
}

h1 {
 padding: 0.5em;
 margin: 0;
}

h2 {
  margin-top: 0.25em;
}

i {
  padding: 0 0.25em 0 0.25em;
}

div {
  margin: 2em ;
  padding: 0 ;
  background: white;
  border-radius: 8px;
}

.main {
  box-shadow: 3px 5px 45px black
}

.form-container {
  width: 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.form {
  padding-bottom: 2em;
}

#result-text {
  padding-left: 1.1em;
  padding-bottom: 2em;
}

//react.js
class App extends React.Component {
  
  render() {
    return (React.createElement(CurrencyConverter, null));
  }  
}

class CurrencyConverter extends React.Component {
  constructor() {
    super();
    
    this.state = {
      baseCurrency:'GBP',
      convertToCurrency:'USD',
      baseAmount: 100,
      rates: [],
      currencies: []
    };
    
    this.changeBaseCurrency = this.changeBaseCurrency.bind(this);
    this.changeConvertToCurrency = this.changeConvertToCurrency.bind(this);
    this.changeBaseAmount = this.changeBaseAmount.bind(this);
    this.getConvertedCurrency = this.getConvertedCurrency.bind(this);
    this.callAPI = this.callAPI.bind(this);
  }
  
  componentDidMount() {
   this.callAPI(this.state.baseCurrency)
  }
  
  changeBaseCurrency(e) {
    this.setState({ baseCurrency: e.target.value});
    this.callAPI(e.target.value)
    
  }
  
 callAPI(base) {
   const api = `https://api.exchangeratesapi.io/latest?base=${base}`;
    
    fetch(api)
     .then(results => {
        return results.json();
    }).then(data => this.setState({
      rates: data['rates'],
      currencies: Object.keys(data['rates']).sort()
    }));
   
 } 
  
  
  changeConvertToCurrency(e) {
    this.setState({
      convertToCurrency: e.target.value
    });
  }
  
  changeBaseAmount(e) {
   this.setState({
     baseAmount: e.target.value
   });
  }
  
  getConvertedCurrency(baseAmount,convertToCurrency,rates) {
      return Number.parseFloat(baseAmount * rates[convertToCurrency]).toFixed(3);
  }
  
  render() {
    const {currencies,rates,baseCurrency,baseAmount,convertToCurrency} = this.state;
    
    const currencyChoice = currencies.map(currency => React.createElement("option", {key: currency, value: currency}, " ", currency, " "));
    
    const result = this.getConvertedCurrency(baseAmount, convertToCurrency, rates);
    
    
    return(
      React.createElement("div", {className: "form-container"}, 
      React.createElement("form", {className: "ui mini form"},
      React.createElement("h3", null, "Convert from:", baseCurrency),
      React.createElement("select", {value: baseCurrency, onChange: this.changeBaseCurrency}, currencyChoice, 
      React.createElement("option", null, baseCurrency)), 
      React.createElement("h3", null, "Convert to:", convertToCurrency), 
      React.createElement("select", {value: convertToCurrency, onChange: this.changeConvertToCurrency}, currencyChoice),
      React.createElement("h3", null, "Amount:"), 
      React.createElement("input", {type: "number", id: "base-amount", defaultValue: baseAmount, onChange: this.changeBaseAmount})),
      React.createElement("h2", {id: "result-text"}, " ", baseAmount," ", baseCurrency, "is equal to ", result, " ", convertToCurrency)));

  }
}


ReactDOM.render(
React.createElement(App, null),
document.getElementById('app')
);
