UPDATE t1 SET t1.Field = t2.Field
FROM Table1 as t1
INNER JOIN Table2 as t2 on t1.Key = t2.Key
WHERE t2.FilterField = 'abc'

UPDATE t1 SET t1.Field = t2.Field
FROM (SELECT DISTINCT Table1 as t1
INNER JOIN Table2 as t2 on t1.Key = t2.Key
WHERE t2.FilterField = 'abc') t3
WHERE t1.key = t3.key

https://stackoverflow.com/questions/3422673/evaluating-a-math-expression-given-in-string-form

package com.example.demo;

import java.io.Serializable;
import java.math.BigDecimal;
import java.math.RoundingMode;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Stack;

public class Eval {

    public static void main(String[] args) {
        FormulaEvaluateReq formulaObj  = new FormulaEvaluateReq();
        
        
          KiVarVal varA = new  KiVarVal();
        varA.setKiVarValNum(1);
        varA.setVarId("A");
        varA.setVarVal(new BigDecimal("100"));

         KiVarVal varB = new  KiVarVal();
        varB.setKiVarValNum(2);
        varB.setVarId("B");
        varB.setVarVal(new BigDecimal("200"));

        formulaObj.setlVariables(Arrays.asList(varA, varB));
        formulaObj.setCalcFormula("100-A/B*(C+D)");
        System.out.println(evaluateFormula(formulaObj));
    }
    
    public static BigDecimal evaluateFormula(FormulaEvaluateReq payLoad) {
//      FormulaEvaluateReq payLoad = request.getPayLoad();
      List<KiVarVal> lVariables = payLoad.getlVariables();
      Map<String, BigDecimal> vars = new HashMap<>();
      lVariables.stream().forEach(var -> {
        vars.put(var.getVarId().toUpperCase(), var.getVarVal());
      });
      String formula = payLoad.getCalcFormula().replaceAll(" ", "");
      BigDecimal dResult = new BigDecimal(0);
      Stack<Object> operationStack = new Stack<>();
      if (formula.indexOf("100") > -1) {
        formula = formula.replaceAll("100", Const.PERCENT_CHAR);
        vars.put(Const.PERCENT_CHAR, new BigDecimal(100));
      }
      String[] split = formula.split("");
      BigDecimal first = getVariableValue(split[0], vars);
      dResult = first;
      for (int i = 1; i < split.length; i++) {
        String current = split[i];
//        logger.info(current);
        switch (current) {
        case "+":
        case "-":
        case "*":
        case "/":
          operationStack.push(current);
          break;
        default:
          Object pop = operationStack.pop();
          dResult = operate((String) pop, getVariableValue(current, vars), dResult);
          break;
        }
      }
      return dResult.setScale(5, RoundingMode.HALF_UP);
    }

    private static BigDecimal operate(String operator, BigDecimal fOperand, BigDecimal res) {
      switch (operator) {
      case "+":
        return res.add(fOperand);
      case "-":
        return res.subtract(fOperand);
      case "*":
        return res.multiply(fOperand);
      case "/":
        return res.divide(fOperand, 10,
            RoundingMode.HALF_UP);/*
                         * Precision should not be lost,
                         * rounding till 10 decimals
                         */
      default:
        return res;
      }
    }

    private static BigDecimal getVariableValue(String string, Map<String, BigDecimal> vars) {
      try {
        return new BigDecimal(string);
      } catch (NumberFormatException nfe) {
//        sys("Failed to convert" + vars.get(string.toUpperCase()));
        return vars.get(string);
      }
    }
}


class KiVarVal implements Serializable {
    private static final long serialVersionUID = 1L;

    private Integer kiVarValNum;

    private String varId;

    private BigDecimal varVal;

    public KiVarVal(Integer kiVarValNum, String varId, BigDecimal varVal) {
        super();
        this.kiVarValNum = kiVarValNum;
        this.varId = varId;
        this.varVal = varVal;
    }

    public KiVarVal() {
    }

    public Integer getKiVarValNum() {
        return kiVarValNum;
    }

    public void setKiVarValNum(Integer kiVarValNum) {
        this.kiVarValNum = kiVarValNum;
    }

    public String getVarId() {
        return varId;
    }

    public void setVarId(String varId) {
        this.varId = varId;
    }

    public BigDecimal getVarVal() {
        return varVal;
    }

    public void setVarVal(BigDecimal varVal) {
        this.varVal = varVal;
    }
}


class FormulaEvaluateReq {
    
    List<KiVarVal> lVariables = new ArrayList<>();
    String calcFormula;
    
    public List<KiVarVal> getlVariables() {
        return lVariables;
    }
    public void setlVariables(List<KiVarVal> lVariables) {
        this.lVariables = lVariables;
    }
    public String getCalcFormula() {
        return calcFormula;
    }
    public void setCalcFormula(String calcFormula) {
        this.calcFormula = calcFormula;
    }
}

class Const {

    public static final String REQ_RES_DATE_FORMAT = "yyyy-MM-dd";
    public static final String REQ_RES_DATE_TIME_FORMAT = "yyyy-MM-dd HH:mm:ss";
    public static final String SORT_COL_SEPARATOR = ",";
    public static final String HYPHEN = "-";
    public static final String DEACTIVATION_FLAG = "Y";
    public static final String YES_FLAG = "Y";
    public static final String NOT_DELETED_FLAG = "N";
    public static final String DASH = "-";
    public static final String PERCENT_CHAR = "%";
}
