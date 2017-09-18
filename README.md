# codes

## 문제1


'''


import java.util.ArrayList;
import java.util.Collections;

class Solution {

	public static ArrayList<String> fromNumToEng = new ArrayList<String>();
	public static ArrayList<String> inputNumber = new ArrayList<String>();
	public static ArrayList<String> inputEnglish = new ArrayList<String>();

	public int[] solution(int[] numbers) {
		int[] answer = new int[numbers.length];

		for (int i = 0; i < numbers.length; i++) {
			inputNumber.add(numbers[i] + "");
		}
		transNumToEng();
		Collections.sort(inputEnglish);
		for (int j = 0; j < inputEnglish.size(); j++) {
			String input = inputEnglish.get(j);
			answer[j] = Integer.parseInt(transEngToNum(input));
		}

		return answer;
	}

	public static void init() {
		fromNumToEng.add("zero");
		fromNumToEng.add("one");
		fromNumToEng.add("two");
		fromNumToEng.add("three");
		fromNumToEng.add("four");
		fromNumToEng.add("five");
		fromNumToEng.add("six");
		fromNumToEng.add("seven");
		fromNumToEng.add("eight");
		fromNumToEng.add("nine");
	}
	
	public String transEngToNum(String input) {
		String temp = "";
		String result = "";
		
		for (int i = 0 ; i < input.length() ; i++) {
			temp += input.charAt(i);
			
			if (temp.length() < 3)
				continue;
				
			for (int j = 0 ; j < 10 ; j++) {
				if (fromNumToEng.get(j).equals(temp)) {
					result += String.valueOf(j);
					temp = "";
					break;
				}
			}
		}
		
		

		return result;
		
	}

	public void transNumToEng() {

		for (String s : inputNumber) {
			String engNum = "";

			if (s.length() == 1) {
				engNum = fromNumToEng.get(Integer.parseInt(s));
				inputEnglish.add(engNum);
			} else {
				String temp = new String();
				for (int i = 0; i < s.length(); i++) {
					temp = fromNumToEng.get(Integer.parseInt(s.charAt(i) + ""));
					engNum += temp;
				}
				inputEnglish.add(engNum);
			}

		}
	}
	
	public static void main (String[] args) {
		
		init();
	
		int[] input1 = {6, 1, 8};
		int[] input2 = {5, 4, 11};
		
		int[] result = new Solution().solution(input1);
		for (int i = 0 ; i < result.length ; i++)
			System.out.print(result[i] + " ");
	}

}
'''

## 문제2
'''

import java.util.ArrayList;

public class CalcFarmArea {
	
	public static int table1[][] = { {0,0,1,1}, {1,1,1,1}, {2,2,2,1}, {0,0,0,2} };
	public static int table2[][] = { {0,0,1}, {2,2,1}, {0,0,0} };
	public static int check1[][];
	public static int check2[][];
	public static ArrayList<Integer> result = new ArrayList<Integer>();
	
	public static void init1() {
		check1 = new int[table1.length][table1.length];
		for (int y = 0 ; y < 4 ; y++) {
			for (int x = 0 ; x < 4 ; x++) {
				check1[y][x] = 0;
			}
		}
		
		result.clear();
		for (int i = 0 ; i < 3 ; i++)
			result.add(0);
	}
	
	public static void init2() {
		check2 = new int[table2.length][table2.length];
		for (int y = 0 ; y < 3 ; y++) {
			for (int x = 0 ; x < 3 ; x++) {
				check2[y][x] = 0;
			}
		}
		
		result.clear();
		for (int i = 0 ; i < 3 ; i++)
			result.add(0);
	}
	
	
	public static void print(int[][] input) {
		for (int y = 0 ; y < input.length ; y++) {
			for (int x = 0 ; x < input.length ; x++) {
				System.out.print(input[y][x] + " ");
			}
			System.out.println();
		}
	}
	
	public static void calc(int[][] inputTable, int[][] inputCheck, int y, int x, int prevValue, int depth) {
		
		if (y < 0) return;
		if (y >= inputTable.length) return;
		if (x < 0) return;
		if (x >= inputTable.length) return;
		if (inputCheck[y][x] == -1) return;
		if (inputTable[y][x] != prevValue) return;
		
		inputCheck[y][x] = -1;
		
		calc(inputTable, inputCheck, y+1, x, inputTable[y][x], depth+1);
		calc(inputTable, inputCheck, y-1, x, inputTable[y][x], depth+1);
		calc(inputTable, inputCheck, y, x+1, inputTable[y][x], depth+1);
		calc(inputTable, inputCheck, y, x-1, inputTable[y][x], depth+1);
		
		if (depth == 0)
			result.set(inputTable[y][x], result.get(inputTable[y][x]) + 1 );
			
	}

	public static void main(String[] args) {
		init1();
		print(table1);
		//System.out.println(result);
		for (int y = 0 ; y < 4 ; y++ ) 
			for (int x = 0 ; x < 4 ; x++ )
				//calc(table1, check1, 0, 0, table1[0][0], 0);
				if (check1[y][x] != -1)
					calc(table1, check1, y, x, table1[y][x], 0);
		System.out.println(result);
		
		init2();
		print(table2);
		for (int y = 0 ; y < 3 ; y++ ) 
			for (int x = 0 ; x < 3 ; x++ )
				//calc(table1, check1, 0, 0, table1[0][0], 0);
				if (check2[y][x] != -1)
					calc(table2, check2, y, x, table2[y][x], 0);
		
		System.out.println(result);
	}

}


'''
