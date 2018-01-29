#months
package com.example.demo;

import java.util.Arrays;
import java.util.List;

import org.joda.time.DateTime;
import org.joda.time.Months;
import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TestName;


//@RunWith(SpringJUnit4ClassRunner.class)
public class TestTest {

    @Rule public TestName name = new TestName();
    
    @Before
    public void printName() {
        
       System.out.println("\n===============================================================================================================\n");
       System.out.println("\n\t" + name.getMethodName() );
    }


   /* @Test
    public void t1() {

        DateTime effectiveFrom = new DateTime(2017, 12, 29, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 1, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void t2() {

        DateTime effectiveFrom = new DateTime(2017, 12, 28, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 1, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void t3() {

        DateTime effectiveFrom = new DateTime(2017, 12, 27, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 1, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }*/
    
  //  @Test
    public void t1Q() {

        DateTime effectiveFrom = new DateTime(2018, 3, 27, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void sameDateQ() {

        DateTime effectiveFrom = new DateTime(2018, 3, 29, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void sameDateQ2() {

        DateTime effectiveFrom = new DateTime(2018, 3, 27, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void beforeAfterQ() {

        DateTime effectiveFrom = new DateTime(2017, 5, 27, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void beforeAfterQ2() {

        DateTime effectiveFrom = new DateTime(2017, 6, 29, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void beforeAfterQ3() {

        DateTime effectiveFrom = new DateTime(2017, 6, 28, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    @Test
    public void beforeAfterQ4() {

        DateTime effectiveFrom = new DateTime(2017, 6, 28, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 3, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
   // @Test
    public void t3() {

        DateTime effectiveFrom = new DateTime(2017, 12, 27, 0, 0, 0, 0);
        DateTime currentDtTm = new DateTime(2018, 1, 29, 0, 0, 0, 0);
       
        generate(effectiveFrom, currentDtTm);
    }
    
    public static void generate(DateTime effectiveFrom, DateTime currentDtTm){
        int freqNum = 2;
        // DateTime currentDtTm = new DateTime();
        System.out.println(Months.monthsBetween(currentDtTm, effectiveFrom).getMonths());
        System.out.println("effectiveFrom\t" + effectiveFrom);
        System.out.println("currentDtTm\t" + currentDtTm + "\n");
        if (!currentDtTm.isBefore(effectiveFrom)) {
            


            switch (freqNum) {
                case 1:
                    /**
                     * MONTH
                     */
                    DateTime roundedMEffFrom = effectiveFrom.getDayOfMonth() <= 28 ? effectiveFrom : effectiveFrom.plusMonths(1);
                    DateTime roundedMCurr = currentDtTm.getDayOfMonth() < 28 ? currentDtTm.minusMonths(1) : currentDtTm;
                    
                    // 28th
                    if (!roundedMCurr.isBefore(roundedMEffFrom)) {
                        DateTime assmentFor = roundedMEffFrom;
                        while(true){
                            addAssessment(assmentFor);
                            if (assmentFor.getYear() == roundedMCurr.getYear()
                                    && assmentFor.getMonthOfYear() == roundedMCurr.getMonthOfYear()){
                                break;                                
                            }
                            assmentFor = assmentFor.plusMonths(1);
                        }
                    }
                    /**
                     * MONTH - END
                     */
                    break;
                case 2:
                    /**
                     * QUARTER
                     */
                    List<Integer> quarterMonths = Arrays.asList(new Integer[] { 3, 6, 9, 12 });
                    // If is quarter end
                    DateTime roundedEffFrom;
                    DateTime roundedCurr;

                    // 28th
                    if (!quarterMonths.contains(effectiveFrom.getMonthOfYear())
                            || effectiveFrom.getDayOfMonth() <= 28) {// That month
                        roundedEffFrom =  !quarterMonths.contains(effectiveFrom.getMonthOfYear()) ? effectiveFrom.withMonthOfYear(
                                quarterMonths.get((int) Math.ceil(effectiveFrom.getMonthOfYear() / 3))) : effectiveFrom;
                        addAssessment(roundedEffFrom);
                        roundedEffFrom = getNextQuarter(roundedEffFrom);
                    } else {
                        roundedEffFrom = effectiveFrom;
                    }

                    if (!quarterMonths.contains(currentDtTm.getMonthOfYear())
                            || (quarterMonths.contains(currentDtTm.getMonthOfYear())
                                    && currentDtTm.getDayOfMonth() < 28)) {// BEFORE
                        roundedCurr = getPreviousQuarter(currentDtTm);

                    } else {
                        roundedCurr = currentDtTm;
                    }

                    System.out.println("\nroundedEffFrom\t" + roundedEffFrom);
                    System.out.println("roundedCurr\t" + roundedCurr + "\n");
                    // All future months

                    // make it current quarter

                    if (roundedCurr.isAfter(roundedEffFrom)) {
                        DateTime assmentFor = roundedEffFrom;
                        while(true){
                            addAssessment(assmentFor);
                            if (assmentFor.getYear() == roundedCurr.getYear()
                                    && assmentFor.getMonthOfYear() == roundedCurr.getMonthOfYear()){
                                break;                                
                            }
                            assmentFor = assmentFor.plusMonths(3);
                        }
                    }
                    /**
                     * QUARTER - END
                     */
                    break;
                case 3:
                    /**
                     * HALF YEAR
                     */

                    List<Integer> halfYearMonths = Arrays.asList(new Integer[] { 6, 12 });
                    DateTime roundedEffFromHY;
                    DateTime roundedCurrHY;

                    // 28th
                    if (!halfYearMonths.contains(effectiveFrom.getMonthOfYear())
                            || effectiveFrom.getDayOfMonth() <= 28) {// That
                        roundedEffFromHY = !halfYearMonths.contains(effectiveFrom.getMonthOfYear())
                                ? effectiveFrom.withMonthOfYear(
                                        halfYearMonths.get((int) Math.ceil(effectiveFrom.getMonthOfYear() / 6)))
                                : effectiveFrom;
                        addAssessment(roundedEffFromHY);
                        roundedEffFromHY = getNextHalfYear(roundedEffFromHY);
                    } else {
                        roundedEffFromHY = effectiveFrom;
                    }

                    if (!halfYearMonths.contains(currentDtTm.getMonthOfYear())
                            || (halfYearMonths.contains(currentDtTm.getMonthOfYear())
                                    && currentDtTm.getDayOfMonth() < 28)) {// BEFORE
                        roundedCurrHY = getPreviousHalfYear(currentDtTm);
                    } else {
                        roundedCurrHY = currentDtTm;
                    }

                    System.out.println("\nroundedEffFrom\t" + roundedEffFromHY);
                    System.out.println("roundedCurrHY\t" + roundedCurrHY + "\n");
                    // All future months

                    // make it current quarter

                    if (roundedCurrHY.isAfter(roundedEffFromHY)) {
                        DateTime assmentForMonthHY = roundedEffFromHY;
                        while (true) {
                            addAssessment(assmentForMonthHY);
                            if (assmentForMonthHY.getYear() == roundedCurrHY.getYear()
                                    && assmentForMonthHY.getMonthOfYear() == roundedCurrHY.getMonthOfYear()) {
                                break;
                            }
                            assmentForMonthHY = assmentForMonthHY.plusMonths(6);
                        }                      
                    }

                    /**
                     * HALF YEAR - END
                     */

                    break;
                case 4:

                    /**
                     * ANNUAL
                     */
                    List<Integer> yearsMonths = Arrays.asList(new Integer[] { 12 });
                    DateTime roundedEffFromY;
                    DateTime roundedCurrY;

                    // 28th
                    if (!yearsMonths.contains(effectiveFrom.getMonthOfYear())
                            || (yearsMonths.contains(effectiveFrom.getMonthOfYear())
                                    && effectiveFrom.getDayOfMonth() <= 28)) {// this year
                        roundedEffFromY = !yearsMonths.contains(effectiveFrom.getMonthOfYear())
                                ? effectiveFrom.withMonthOfYear(12)
                                : effectiveFrom;
                        addAssessment(roundedEffFromY);
                        roundedEffFromY = roundedEffFromY.plusYears(1).withMonthOfYear(12);
                    } else {
                        roundedEffFromY = effectiveFrom;
                    }

                    if (!yearsMonths.contains(currentDtTm.getMonthOfYear())
                            || (yearsMonths.contains(currentDtTm.getMonthOfYear())
                                    && currentDtTm.getDayOfMonth() < 28)) {// BEFORE
                        roundedCurrY = currentDtTm.minusYears(1).withMonthOfYear(12);
                    } else {
                        roundedCurrY = currentDtTm;
                    }

                    System.out.println("\nroundedEffFrom\t" + roundedEffFromY);
                    System.out.println("roundedCurrY\t" + roundedCurrY + "\n");
                    // All future months

                    // make it current quarter

                    if (roundedCurrY.isAfter(roundedEffFromY)) {
                        DateTime assmentForMonthY = roundedEffFromY;
                        while (true) {
                            addAssessment(assmentForMonthY);
                            if (assmentForMonthY.getYear() == roundedCurrY.getYear()
                                    && assmentForMonthY.getMonthOfYear() == roundedCurrY.getMonthOfYear()){
                                break;
                            }
                            assmentForMonthY = assmentForMonthY.plusMonths(12);
                        }                        
                    }
                    
                    /**
                     * ANNUAL END
                     */
                    break;
                default:

            }
        }
    }

    private static DateTime getPreviousHalfYear(DateTime roundedCurr) {
        int locForMonth = roundedCurr.getMonthOfYear();
        int previousQuarterMonth;
        int previousQuarterYear = roundedCurr.getYear();

        if (locForMonth <= 12 && locForMonth >= 7) {// Q4
            previousQuarterMonth = 6;
        } else {// Q1
            previousQuarterMonth = 12;
            previousQuarterYear--;
        }
        return roundedCurr.withYear(previousQuarterYear).withMonthOfYear(previousQuarterMonth);
    }

    private static DateTime getPreviousQuarter(DateTime roundedCurr) {
        int locForMonth = roundedCurr.getMonthOfYear();
        int previousQuarterMonth;
        int previousQuarterYear = roundedCurr.getYear();

        if (locForMonth <= 12 && locForMonth >= 10) {// Q4
            previousQuarterMonth = 9;
        } else if (locForMonth <= 9 && locForMonth >= 7) {// Q3
            previousQuarterMonth = 6;
        } else if (locForMonth <= 6 && locForMonth >= 4) {// Q2
            previousQuarterMonth = 3;
        } else {// Q1
            previousQuarterMonth = 12;
            previousQuarterYear--;
        }
        return roundedCurr.withYear(previousQuarterYear).withMonthOfYear(previousQuarterMonth);
    }

    private static DateTime getNextQuarter(DateTime roundedCurr) {
        int locForMonth = roundedCurr.getMonthOfYear();
        int previousQuarterMonth;
        int previousQuarterYear = roundedCurr.getYear();

        if (locForMonth <= 12 && locForMonth >= 10) {// Q4
            previousQuarterMonth = 3;
            previousQuarterYear++;
        } else if (locForMonth <= 9 && locForMonth >= 7) {// Q3
            previousQuarterMonth = 12;
        } else if (locForMonth <= 6 && locForMonth >= 4) {// Q2
            previousQuarterMonth = 9;
        } else {// Q1
            previousQuarterMonth = 6;

        }
        return roundedCurr.withYear(previousQuarterYear).withMonthOfYear(previousQuarterMonth);
    }

    private static void addAssessment(DateTime assmentFor) {
        System.out.println("Adding assessment for \t" + assmentFor);
    }
    
    public static DateTime getNextHalfYear(DateTime roundedCurr) {
        int locForMonth = roundedCurr.getMonthOfYear();
        int previousQuarterMonth;
        int previousQuarterYear = roundedCurr.getYear();

        if (locForMonth <= 12 && locForMonth >= 7) {// Q4
            previousQuarterMonth = 6;
            previousQuarterYear++;
        } else {// Q1
            previousQuarterMonth = 12;
        }
        return roundedCurr.withYear(previousQuarterYear).withMonthOfYear(previousQuarterMonth);
    }
}
