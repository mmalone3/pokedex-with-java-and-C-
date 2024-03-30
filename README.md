# pokedex-with-java-and-C-sharp
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class Pokedex {

    public static void main(String[] args) {
        List<String> pokemonNames = fetchPokemonNames();
        pokemonNames.forEach(System.out::println);
    }

    private static List<String> fetchPokemonNames() {
        List<String> pokemonNames = new ArrayList<>();
        String url = "https://pokemondb.net/pokedex/all";

        try {
            Document document = Jsoup.connect(url).get();
            Elements pokemonElements = document.select("span.infocard-lg-data");

            for (Element element : pokemonElements) {
                pokemonNames.add(element.text());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        return pokemonNames;
    }
}
