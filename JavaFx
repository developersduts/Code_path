import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.logging.Level;
import java.util.logging.Logger;
import javafx.application.Application;
import javafx.beans.property.SimpleStringProperty;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.stage.FileChooser;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.VBox;

public class Main extends Application {
	TableView table = new TableView();
	List<Footballers> list = new ArrayList<>();
	ObservableList<Footballers> data;
	String o = "";
	String[] m;

	public void start(Stage primaryStage) {
		FileChooser fileChooser = new FileChooser();
		Button buttonopen = new Button("OPEN FILE");
		buttonopen.setOnAction(new EventHandler<ActionEvent>() {
			public void handle(ActionEvent arg0) {
				FileChooser.ExtensionFilter extFilter = new FileChooser.ExtensionFilter("TXT files (*.txt)", "*.txt");
				fileChooser.getExtensionFilters().add(extFilter);
				File file = fileChooser.showOpenDialog(primaryStage);
				if (file != null) {
					openFile(file);
				}
				data = FXCollections.observableArrayList(list);
				table.setItems(data);
				System.out.println(list);
			}
		});

		Button buttonsave = new Button("SAVE FILE");
		buttonsave.setOnAction(new EventHandler<ActionEvent>() {
			public void handle(ActionEvent arg0) {
				FileChooser.ExtensionFilter extFilter = new FileChooser.ExtensionFilter("Файл RTF", "*.rtf");
				fileChooser.getExtensionFilters().add(extFilter);

				File file1 = fileChooser.showSaveDialog(primaryStage);
				if (file1 != null) {
					SaveFile(table.getItems(), file1);
				}
			}
		});

		TableColumn mCol = new TableColumn("Footballers");
		mCol.setMinWidth(100);
		mCol.setCellValueFactory(new PropertyValueFactory<Footballers, String>("Footballers"));

		TableColumn dCol = new TableColumn("Country");
		dCol.setMinWidth(100);
		dCol.setCellValueFactory(new PropertyValueFactory<Footballers, String>("Country"));

		TableColumn pCol = new TableColumn("Age");
		pCol.setMinWidth(100);
		pCol.setCellValueFactory(new PropertyValueFactory<Footballers, String>("Age"));

		data = FXCollections.observableArrayList(list);
		table.setItems(data);
		table.getColumns().addAll(mCol, dCol, pCol);

		VBox v = new VBox();
		v.getChildren().addAll(buttonopen, table, buttonsave);
		Scene scene = new Scene(v, 300, 300);
		primaryStage.setScene(scene);
		primaryStage.show();

	}

	public static void main(String[] args) {
		launch(args);
	}

	public class Footballers {
		private SimpleStringProperty Footballers;
		private SimpleStringProperty Country;
		private SimpleStringProperty Age;

		private Footballers(String m, String d, String p) {
			this.Footballers = new SimpleStringProperty(m);
			this.Country = new SimpleStringProperty(d);
			this.Age = new SimpleStringProperty(p);
		}

		public String getFootballers() {
			return Footballers.get();
		}

		public String getCountry() {
			return Country.get();
		}

		public String getAge() {
			return Age.get();
		}

		public String toString() {
			return this.Footballers.getValue() + " " + this.Country.getValue() + " " + this.Age.getValue();
		}
	}

	private void SaveFile(ObservableList<Footballers> d, File file) {
		try {
			FileWriter fileWriter;
			fileWriter = new FileWriter(file);
			fileWriter.write(d.toString());
			fileWriter.close();
		} catch (IOException ex) {
		}
	}

	private String openFile(File file) {
		BufferedReader bufferedReader = null;
		StringBuilder sb = new StringBuilder();
		try {
			bufferedReader = new BufferedReader(new FileReader(file));
			String text = "";
			while ((text = bufferedReader.readLine()) != null) {
				o += text + " " + "\n";
			}
			m = o.split(" ");
			for (int j = 0; j < m.length - 1; j++) {
				String a = m[j++].trim();
				String b = m[j++].trim();
				String c = m[j].trim();
				Footballers p = new Footballers(a, b, c);
				list.add(p);
			}
		} catch (FileNotFoundException ex) {
			Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
		} catch (IOException ex) {
			Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
		} finally {
			try {
				bufferedReader.close();
			} catch (IOException ex) {
				Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
			}
		}
		return sb.toString();
	}
}








