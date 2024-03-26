

# Algo banques

## BNC

```javascript
var mortgageLoanAmount = price - parseInt(downpayment);

var downPaymentPercent = Number(parseInt(downpayment) / (price));

var insurancePremiumPercentage = Number(downPaymentPercent * 100) < 10 ?
    Number(4 / 100): Number(downPaymentPercent * 100) < 15 ?
        Number(3.1 / 100) : Number(downPaymentPercent * 100) < 20 ? Number(2.8 / 100) : 0;

var insurancePremiumAmount  = insurancePremiumPercentage * mortgageLoanAmount;

var totalMortgageAmount = mortgageLoanAmount + insurancePremiumAmount;

var effectiveMonthlyMortgageRate =(Math.pow((1 + rate / 200), 1 / 6) - 1) * 100;

var monthlyPaymentAmount =  Number(((mortgageLoanAmount * effectiveMonthlyMortgageRate) / 100) / (1 - (Math.pow(1 + effectiveMonthlyMortgageRate/100, (0 - Number(this.actualValues.repaymentPeriod) * 12 )))));

var monthlyInsurancePremiumAmount = Number(((insurancePremiumAmount * effectiveMonthlyMortgageRate) / 100) / (1 - (Math.pow(1 + effectiveMonthlyMortgageRate/100, (0 - Number(this.actualValues.repaymentPeriod) * 12 )))));

var monthlyPaymentTotal = monthlyPaymentAmount + monthlyInsurancePremiumAmount;

var monthlyPaymentPeriods = Number(((Math.log(monthlyPaymentAmount)-Math.log(monthlyPaymentAmount-(mortgageLoanAmount*effectiveMonthlyMortgageRate/100)))/(Math.log(1+effectiveMonthlyMortgageRate/100)))/(12)*12);

var monthlyCumulativePayment = monthlyPaymentPeriods * monthlyPaymentTotal;

//Monthly Calculation
var effectiveBiWeeklyMortgageRate = (Math.pow(1 + rate / 200, 28 / 365) - 1) * 100;

var biWeeklyPaymentAmount = (monthlyPaymentAmount / 2);

var biWeeklyInsurancePremiumAmount = Number(monthlyInsurancePremiumAmount / 2);

var biWeeklyPaymentTotal = Number(biWeeklyPaymentAmount) + Number(biWeeklyInsurancePremiumAmount);

var biWeeklyPaymentPeriods  = ((Math.log(biWeeklyPaymentAmount) - Math.log(biWeeklyPaymentAmount-(mortgageLoanAmount * effectiveBiWeeklyMortgageRate/100))) / (Math.log(1 + effectiveBiWeeklyMortgageRate / 100)))/(26)*12;

var biWeeklyPaymentYears = Math.floor(biWeeklyPaymentPeriods/12);

var biWeeklyPaymentMonths  = Math.ceil(biWeeklyPaymentPeriods) % 12;

var biWeeklyPaymentNumber = biWeeklyPaymentPeriods / 12 * 26;

var biWeeklyCumulativePayment  = Number(biWeeklyPaymentTotal * biWeeklyPaymentNumber);

var biWeeklySavings = monthlyCumulativePayment - biWeeklyCumulativePayment ;

var effectiveWeeklyMortgageRate = (Math.pow(1 + (rate ) / 200, 14 / 365) - 1) * 100;

//Weekly Calculation
var weeklyPaymentAmount = monthlyPaymentAmount / 4;

var weeklyInsurancePremiumAmount = monthlyInsurancePremiumAmount / 4;

var weeklyPaymentTotal = weeklyPaymentAmount + weeklyInsurancePremiumAmount;

var weeklyPaymentPeriods = ((Math.log(weeklyPaymentAmount) - Math.log(weeklyPaymentAmount - (mortgageLoanAmount * effectiveWeeklyMortgageRate / 100))) / (Math.log(1 + effectiveWeeklyMortgageRate / 100)))/(52)*12;

var weeklyPaymentYears = Math.floor(weeklyPaymentPeriods / 12);

var weeklyPaymentMonths = Math.ceil(weeklyPaymentPeriods % 12);

var weeklyPaymentNumber = weeklyPaymentPeriods / 12 * 52;

var weeklyCumulativePayment = weeklyPaymentTotal * weeklyPaymentNumber;

var weeklySavings = monthlyCumulativePayment - weeklyCumulativePayment;

```

| Paramètre | Scenario 1 | Scenario 2 |
| --- | --- | --- |
| Valeur de la propriété | 250 000 | 250 000 |
| Mise de fond | 50 000 | 12 500 |
| Taux | 5% | 5% |
| Durée de remboursement | 25 ans | 25 ans |

| Variable | Scenario 1 | Scenario 2 |
| --- | --- | --- |
| mortgageLoanAmount | 200000 | 237500 |
| downPaymentPercent | 0.2 | 0.05 |
| insurancePremiumPercentage | 0 | 0.04 |
| insurancePremiumAmount | 0 | 9500 |
| totalMortgageAmount | 200000 | 247000 |
| effectiveMonthlyMortgageRate | 0.41239154651442345 | 0.41239154651442345 |
| monthlyPaymentAmount | 1163.2099700740312 | 1381.311839462912 |
| monthlyInsurancePremiumAmount | 0 | 55.25247357851648 |
| monthlyPaymentTotal | 1163.2099700740312 | 1436.5643130414285 |
| monthlyPaymentPeriods | 299.9999999999999 | 299.9999999999999 |
| monthlyCumulativePayment | 348962.99102220923 | 430969.2939124284 |
| effectiveBiWeeklyMortgageRate | 0.18960229979758658 | 0.18960229979758658 |
| biWeeklyPaymentAmount | 581.6049850370156 | 690.655919731456 |
| biWeeklyInsurancePremiumAmount | 0 | 27.62623678925824 |
| biWeeklyPaymentTotal | 581.6049850370156 | 718.2821565207142 |
| biWeeklyPaymentPeriods | 257.18870297619264 | 257.18870297619264 |
| biWeeklyPaymentYears | 21 | 21 |
| biWeeklyPaymentMonths | 6 | 6 |
| biWeeklyPaymentNumber | 557.2421897817508 | 557.2421897817508 |
| biWeeklyCumulativePayment | 324094.835450009 | 400257.12178076105 |
| biWeeklySavings | 24868.155572200252 | 30712.17213166732 |
| effectiveWeeklyMortgageRate | 0.09475625615837924 | 0.09475625615837924 |
| weeklyPaymentAmount | 290.8024925185078 | 345.327959865728 |
| weeklyInsurancePremiumAmount | 0 | 13.81311839462912 |
| weeklyPaymentTotal | 290.8024925185078 | 359.1410782603571 |
| weeklyPaymentPeriods | 256.97262149507577 | 256.9726214950755 |
| weeklyPaymentYears | 21 | 21 |
| weeklyPaymentMonths | 5 | 5 |
| weeklyPaymentNumber | 1113.5480264786615 | 1113.5480264786604 |
| weeklyCumulativePayment | 323822.5416390601 | 399920.8389242388 |
| weeklySavings | 25140.449383149156 | 31048.454988189565 |


## Desjardins

```javascript
angular.module('calculHypo').factory(
  'CalculHypo',
  function () {
    return {
      calculateABD: function (e, t, r, n) {
        return 0.32 * e - (t + r + 0.5 * n)
      },
      calculateATD: function (e, t, r, n, a) {
        return 0.4 * e - (t + r + 0.5 * n + a)
      },
      maxValueFromMiseFond: function (e) {
        return e < 25000 ? e / 0.05 : 500000 + (e - 25000) / 0.1
      },
      ratioPV: function (e, t) {
        return 1 - e / t
        // 0.8
      },
      financingWithSCHL: function (e, t, r) {
        return e * t * (1 + r)
      },
      payment: function (e, t, r) {
        return r / ((1 - Math.pow(1 + e, - 1 * t)) / e)
        // 1163.2099700740312
      },
      monthlySCHL: function (e, t, r, n) {
        var a = this.maxValueFromMiseFond(e),
        i = this.ratioPV(e, a),
        e = this.getSCHLRate(i),
        e = this.financingWithSCHL(a, i, e),
        n = this.monthlyRate(t, n);
        return this.payment(n, r, e)
      },
      monthlyRate: function (e, t) {
        return this.effectiveRate(e, t = t || 2, 12)
      },
      effectiveRate: function (e, t, r) {
        return Math.pow(1 + e / t, t / r) - 1
        // 0.0041239154651442345
      },
      getSCHLRate: function (e) {
        return e <= 0.8 ? 0 : e <= 0.85 ? 0.028 : e <= 0.9 ? 0.031 : e <= 0.95 ? 0.04 : 0
        // 0
      },
      presentValue: function (e, t, r) {
        return e * ((1 - Math.pow(1 + r, - t)) / r)
      },
      futurValue: function (e, t, r) {
        return e * ((Math.pow(1 + r, t) - 1) / r)
      },
      premiumSCHL: function (e, t) {
        return e * t
      },
      premiumSCHLWithLimit: function (e, t) {
        return e - e / (1 + t)
      },
      interest: function (e, t, r, n, a) {
        for (var i, o, s = 0, u = 0; 0 < e; ) {
          if ((i = r) < (o = this.round(e * t, 2))) return console.error('Les int?r?ts sont plus grand que le versement.'),
          0;
          a &&
          u % n == 0 &&
          (i += a),
          e -= (i = e < i - o ? e + o : i) - o,
          s += o,
          u++
        }
        return s
        // 148962.87000000008
      },
    }
  }
);
  d.construireTableau = function () {
  var e = d.montant_pret,
  t = getNombreRemboursementsParAn(d.param.frequence_versements),
  r = getNombreVersementsAnnuels(d.param.frequence_versements),
  n = getTauxPeriodique(d.type_terme_pret.nbCapitalisation, t, d.param.taux_interet),
  a = {};
  d.remboursements = [];
  var i = new Date;
  a[i.getFullYear()] = Math.round(e);
  for (var o, s, u, m, l = Math.ceil(d.param.amortissement * t), c = 0; c < l; c++) 0 < e &&
  (
    o = new Date,
    1 == d.param.frequence_versements ||
    4 == d.param.frequence_versements ? o.setTime(o.getTime() + 604800000 * (c + 1)) : 2 == d.param.frequence_versements ? o.setMonth(o.getMonth() + (c + 1)) : 3 != d.param.frequence_versements &&
    5 != d.param.frequence_versements ||
    o.setTime(o.getTime() + 604800000 * (c + 1) * 2),
    s = d.montant_versement,
    u = montantArrondi(e * n),
    0 < + d.param.montant_anticipe_annuel &&
    1 < c &&
    c % r == 0 &&
    (s += + d.param.montant_anticipe_annuel),
    e -= m = montantArrondi((s = e < s - u ? e + u : s) - u),
    void 0 === a[(i = o).getFullYear()] &&
    (a[i.getFullYear()] = Math.floor(e)),
    d.remboursements.push({
      numero: c + 1,
      date: o,
      versement: s,
      interets: u,
      capital: m,
      solde: e
    })
  );
  0 < a[i.getFullYear()] &&
  (a[i.getFullYear() + 1] = Math.max(0, Math.floor(e)));
  var p,
  _ = [];
  for (p in a) _.push([Date.UTC(parseInt(p), 0, 1),
  a[p]]);
  return _
}
```