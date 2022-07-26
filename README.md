+package com.frontgate.Tests;

import java.io.File;
import java.io.FileInputStream;
import java.util.Arrays;

import org.apache.poi.ss.usermodel.DataFormatter;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.testng.annotations.DataProvider;

public class ExcelDataSupplier {

	@DataProvider (name="loginTestData", parallel = true)
	public String[][]  getData()  throws Exception {
		File excelFile = new File("./src/test/resources/TestData.xlsx");
		System.out.println(excelFile.exists());
		FileInputStream inputStream = new FileInputStream(excelFile);
		XSSFWorkbook workbook = new XSSFWorkbook(inputStream);
		XSSFSheet sheet = workbook.getSheet("Sheet1");
		int noOfRows = sheet.getPhysicalNumberOfRows();
		int noOfColumns = sheet.getRow(0).getLastCellNum();

		String[][] data = new String[noOfRows-1][noOfColumns];
		for (int i = 0; i < noOfRows -1 ; i++) {
			for (int j = 0; j < noOfColumns; j++) {
				DataFormatter df = new DataFormatter();
				data[i][j] = df.formatCellValue(sheet.getRow(i+1).getCell(j));
//				System.out.println( sheet.getRow(i).getCell(j).getStringCellValue());

			}
			System.out.println();

		}

		workbook.close();
		inputStream.close();

		/*
		 * for (String[] dataArr : data) { System.out.println(Arrays.toString(dataArr));
		 * }
		 */
		return data;
	}

}
